# Diário de Bordo – Sprint 1

**Disciplina:** Gestão de Configuração e Evolução de Software
**Projeto:** Contribuição para o repositório open source [KDE Kdenlive](https://invent.kde.org/multimedia/kdenlive)  
**Issue:** [#2172 — Don't allow any clip in the sequence folder](https://invent.kde.org/multimedia/kdenlive/-/work_items/2172)  
**Merge Request:** [!864](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/864/diffs)  
**Responsáveis:** Gustavo Oki e Davi

---

## Sobre o Projeto

A contribuição consistiu em identificar, analisar e corrigir a issue #2172, que permitia que clipes comuns (vídeo, áudio, imagem) fossem inseridos incorretamente dentro da pasta especial **Sequences** que deveria conter apenas sequências (timelines aninhadas).

---

## Entradas do Diário

---

### Entrada 01 — Seleção da Issue

**Responsáveis:** Gustavo e Davi (análise conjunta)

Após explorar o repositório do Kdenlive em busca de uma boa issue para primeira contribuição, selecionamos a **#2172: Don't allow any clip in the sequence folder**.

Os critérios que guiaram a escolha foram:

- Issue recente (criada há poucas semanas);
- Escopo pequeno e bem delimitado, afetando apenas a lógica de validação de drop/import no Project Bin;
- Sem dependência de refactors em andamento ou mudanças de arquitetura;
- Label **First Task**, indicando que foi criada especificamente para novos contribuidores;
- Não envolve timeline, render ou estados globais complexos.

**Problema identificado:** A pasta `Sequences` do Project Bin deveria aceitar apenas *sequence clips* (timelines aninhadas). Porém, era possível inserir qualquer tipo de clipe nela (vídeos, áudios e imagens) por meio de drag externo, drag interno ou botão "Add Clip".

**Estrutura incorreta (antes do fix):**

```
Project Bin
├── Videos
├── Audio
└── Sequences
    ├── timeline1
    ├── timeline2
    └── video.mp4  ❌
```

**Objetivo do fix:** bloquear `video.mp4`, `audio.wav`, `image.png` e qualquer clipe não-sequência, permitindo apenas sequence clips.

---

### Entrada 02 — Exploração do Código-Fonte

**Responsável principal:** Davi  
**Revisão:** Gustavo

Realizamos um mergulho no código-fonte do Kdenlive para mapear a infraestrutura existente e localizar os pontos de mudança necessários.

**Descobertas relevantes:**

- `AbstractProjectItem::SequenceFolder`: já existe como *data role*, usado em `bin.cpp` para renderizar o ícone especial da pasta. É possível chamá-lo via `index.data(AbstractProjectItem::SequenceFolder).toBool()`;
- `SequenceClip`: classe separada de `ProjectClip`, com `#include "sequenceclip.h"` já presente em `projectitemmodel.cpp`;
- `m_sequenceFolderId`: inteiro já armazenado no `ProjectItemModel`, inicializado como `-1`, que rastreia o ID da pasta de sequências.

**Arquivos identificados para modificação:**

| Arquivo | Função relevante |
|---|---|
| `src/bin/projectitemmodel.cpp` | `dropMimeData()`, `canDropMimeData()`, `addItem()`, `requestAddBinClip()` |
| `src/bin/bin.cpp` | `slotItemDropped()`, `slotUrlsDropped()`, `slotAddClip()` |
| `src/bin/projectitemmodel.h` | Declaração de `canDropMimeData()` |

**Fluxo de drop mapeado:**

```
drag item
    ↓
drop folder
    ↓
dropMimeData()  →  emite urlsDropped (arquivos externos)
                →  emite itemDropped (clips internos do bin)
                        ↓
                  slotItemDropped() / slotUrlsDropped()
```

Para clonar e navegar pelo repositório:

```bash
git clone https://invent.kde.org/multimedia/kdenlive.git
cd kdenlive/src/bin
```

---

### Entrada 03 — Como Reproduzir o Bug

**Responsável principal:** Gustavo  
**Revisão:** Davi

Antes de implementar, documentamos os passos para reprodução do bug, garantindo que o fix pudesse ser validado corretamente.

**Cenário A — Drag de arquivo externo:**
1. Abrir o Kdenlive com qualquer projeto
2. Abrir o gerenciador de arquivos do sistema
3. Arrastar um `video.mp4` (ou `.jpg`, `.wav`) para dentro da pasta `Sequences` no bin
4. **Bug:** o arquivo é importado normalmente ❌

**Cenário B — Drag interno no bin:**
1. Importar qualquer clipe normalmente no bin (fora da pasta `Sequences`)
2. Arrastar esse clipe para dentro da pasta `Sequences`
3. **Bug:** o clipe é movido sem nenhum aviso ❌

**Cenário C — Botão "Add Clip" com pasta selecionada:**
1. Clicar na pasta `Sequences` para selecioná-la
2. Usar o botão `+` para importar um arquivo
3. **Bug:** o clipe vai parar dentro da `Sequences` ❌

**Comportamento esperado:** em todos os cenários acima, o Kdenlive deve exibir:
> *"Only sequence clips can be placed in the Sequences folder."*

**Caso permitido (não deve ser quebrado):**
- Criar uma nova sequence (botão *New Sequence*) → deve aparecer dentro da pasta `Sequences` normalmente ✅

---

### Entrada 04 — Primeira Implementação

**Responsável principal:** Davi  
**Revisão:** Gustavo

Com o mapeamento do código concluído, implementamos a primeira versão do fix nos três pontos identificados.

**Fix 1 — `dropMimeData` em `projectitemmodel.cpp`**

Adicionada verificação antes de emitir qualquer sinal: se o destino é a `Sequences folder`, bloquear URLs externas imediatamente (arquivos do sistema nunca serão sequências).

**Fix 2 — `slotItemDropped` em `bin.cpp`**

Adicionada verificação para drags internos: antes de mover o clipe, valida se o destino é a pasta de sequências e se o clipe é do tipo `SequenceClip`.

**Fix 3 (feedback visual) — `canDropMimeData` em `projectitemmodel.cpp`**

Implementado o override de `canDropMimeData`, que faz o cursor mudar para o ícone de bloqueio durante o drag, dando feedback visual imediato antes mesmo do soltar.

Declaração adicionada em `projectitemmodel.h`:

```cpp
bool canDropMimeData(const QMimeData *data, Qt::DropAction action,
                     int row, int column, const QModelIndex &parent) const override;
```

**Observação técnica importante:** o MIME type interno correto é `"text/producerslist"` (não `"kdenlive/producerslist"` como estimado inicialmente, confirmado ao ler o código real).

---

### Entrada 05 — Depuração: Fix Não Funcionava

**Responsável principal:** Gustavo 
**Suporte:** Davi

Após a primeira implementação, o fix não estava surtindo efeito. Adicionamos prints de diagnóstico para identificar o caminho exato pelo qual o clipe estava entrando na pasta:

```cpp
// Em dropMimeData:
qDebug() << ">>> dropMimeData chamado";
qDebug() << " parent válido:" << parent.isValid();
qDebug() << " isSequenceFolder:" << parent.data(AbstractProjectItem::SequenceFolder).toBool();
qDebug() << " hasUrls:" << data->hasUrls();

// Em slotItemDropped:
qDebug() << ">>> slotItemDropped chamado com ids:" << ids;
```

**Bugs encontrados:**

1. **Erro de sintaxe:** `canDropMimeData` foi declarado com `;` após `const override`, tornando-o uma declaração em vez de definição. O bloco `{...}` ficou solto, e o override nunca foi registrado.

2. **`slotUrlsDropped` não coberto:** o caminho de drop de URLs externas passava por `slotUrlsDropped` → `ClipCreator::createClipsFromList`, que não havia sido protegido. Descobrimos também que o código original já redirecionava silenciosamente para a raiz, mas sem exibir mensagem ao usuário.

3. **Header ausente:** o `std::dynamic_pointer_cast<SequenceClip>` em `bin.cpp` exigia `#include "sequenceclip.h"`, que não estava presente.

---

### Entrada 06 — Refatoração e Correção dos Bugs

**Responsável principal:** Davi  
**Revisão:** Gustavo

Com os bugs identificados, realizamos uma refatoração completa da abordagem, corrigindo todos os pontos problemáticos.

**Principais correções:**

**Bug 1 — `getItemById` com argumento errado em `dropMimeData`:**

```cpp
// ERRADO — método errado, parâmetro errado:
std::shared_ptr<AbstractProjectItem> parentItem =
    getItemById(parent.data(AbstractProjectItem::IdRole).toString());

// CORRETO:
std::shared_ptr<AbstractProjectItem> parentItem;
if (parent.isValid()) {
    parentItem = getBinItemByIndex(parent);
    while (parentItem && parentItem->itemType() != AbstractProjectItem::FolderItem) {
        parentItem = std::static_pointer_cast<AbstractProjectItem>(
            parentItem->parentItem().lock());
    }
}
bool isSequenceFolder = parentItem &&
    m_sequenceFolderId >= 0 &&
    parentItem->clipId().toInt() == m_sequenceFolderId;
```

**Bug 2 — Loop com IDs de pasta (`#2`) sendo passados para `getItemById`:**

```cpp
// CORRETO — pular pastas e usar getItemByBinId:
for (const QString &id : ids) {
    if (id.startsWith(QLatin1Char('#'))) {
        continue; // pastas podem ser movidas livremente
    }
    std::shared_ptr<AbstractProjectItem> item = getItemByBinId(id);
    if (!item) continue;
    if (item->itemType() == AbstractProjectItem::ClipItem &&
        item->clipType() != ClipType::Timeline) {
        pCore->displayMessage(
            i18n("Only sequence clips can be placed in the Sequences folder."),
            KMessageWidget::Warning);
        return false;
    }
}
```

**Bug 3 — Cast frágil com `SequenceClip` em `addItem`:**

```cpp
// FRÁGIL — depende de header e pode falhar em runtime:
if (!std::dynamic_pointer_cast<SequenceClip>(item)) { ... }

// ROBUSTO — usando a API existente:
if (item->itemType() == AbstractProjectItem::ClipItem &&
    item->clipType() != ClipType::Timeline) {
    pCore->displayMessage(
        i18n("Only sequence clips can be placed in the Sequences folder."),
        KMessageWidget::Warning);
    return false;
}
```

**Bug 4 — Redirecionamento silencioso em `requestAddBinClip`:**

Removido o redirecionamento silencioso para a raiz. A proteção ficou centralizada em `addItem()`, que é a camada final e mais confiável:

```cpp
// Sem redirecionamento — addItem() já protege a pasta de sequências
bool res = requestAddBinClip(id, description, parentId, undo, redo, readyCallBack);
```

---

### Entrada 07 — Solução Final e Cobertura Completa

**Responsável principal:** Gustavo 
**Revisão:** Davi

Com todos os bugs corrigidos, a solução final cobre os três cenários de entrada da issue:

| Cenário | Onde é bloqueado |
|---|---|
| Drag de arquivo externo do file manager | `dropMimeData()` — bloco `hasUrls()` |
| Drag interno de clip do bin | `dropMimeData()` → `slotItemDropped()` |
| Botão "Add Clip" com pasta selecionada | `slotAddClip()` → redireciona com mensagem |
| Import via drag de URL | `slotUrlsDropped()` → verifica `defaultSequencesFolder()` |
| Fallback final | `addItem()` — camada de proteção definitiva |

**Arquivos modificados:**

- `src/bin/projectitemmodel.cpp` — `dropMimeData()`, `canDropMimeData()`, `addItem()`, `requestAddBinClip()`
- `src/bin/projectitemmodel.h` — declaração de `canDropMimeData()`
- `src/bin/bin.cpp` — `slotItemDropped()`, `slotUrlsDropped()`, `slotAddClip()`

**Mensagem de commit utilizada:**

```
Prevent non-sequence clips from being added to the Sequences folder

The Sequences folder should only contain sequence (nested timeline) clips.
Add validation in dropMimeData(), canDropMimeData(), addItem() and slotItemDropped()
to block regular video/audio/image clips from being dropped or moved there.

BUG: 2172
```

---

### Entrada 08 — Submissão do Merge Request

**Responsáveis:** Gustavo e Davi

O Merge Request [!864](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/864/diffs) foi submetido ao repositório oficial do Kdenlive com a correção completa da issue #2172.

**Cenários testados antes da submissão:**

- [x] Drag de `video.mp4` do file manager para a pasta `Sequences` → bloqueado com mensagem ✅
- [x] Drag interno de clip de vídeo para a pasta `Sequences` → bloqueado com mensagem ✅
- [x] Cursor muda para ícone de bloqueio durante o drag sobre a pasta (`canDropMimeData`) ✅
- [x] Criar nova sequence pelo botão *New Sequence* → aparece corretamente na pasta ✅
- [x] Mover pastas internas continua funcionando normalmente ✅

---

## Resumo Técnico

| Aspecto | Detalhe |
|---|---|
| **Repositório** | [invent.kde.org/multimedia/kdenlive](https://invent.kde.org/multimedia/kdenlive) |
| **Issue** | #2172 — Don't allow any clip in the sequence folder |
| **MR** | !864 |
| **Linguagem** | C++ / Qt |
| **Arquivos modificados** | `src/bin/projectitemmodel.cpp`, `src/bin/projectitemmodel.h`, `src/bin/bin.cpp` |
| **Linhas de código** | ~60–80 linhas adicionadas/modificadas |
| **Tipo de contribuição** | Bug fix + melhoria de UX (feedback visual durante drag) |

---

## Divisão de Contribuições

| Tarefa | Gustavo | Davi |
|---|---|---|
| Seleção e análise da issue | ✅ | ✅ |
| Mapeamento do código-fonte | ✅ | ✅ |
| Documentação de reprodução do bug | ✅ | — |
| Primeira implementação do fix | — | ✅ |
| Diagnóstico e depuração | ✅ | — |
| Refatoração e correção dos bugs | — | ✅ |
| Solução final e cobertura completa | ✅ | — |
| Submissão do Merge Request | ✅ | ✅ |

---

## Plano Pessoal para a Próxima Sprint (Sprint 2)
 
- [ ] Identificar e abrir mais uma issue.
- [ ] Atualizar contribuição conforme a comunidade e revisores.
