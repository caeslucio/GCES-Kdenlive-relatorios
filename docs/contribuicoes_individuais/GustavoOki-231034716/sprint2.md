# Diário de Bordo – Sprint 2

**Disciplina:** Gestão de Configuração e Evolução de Software
**Projeto:** Contribuição para o repositório open source [KDE Kdenlive](https://invent.kde.org/multimedia/kdenlive)  
**Issue:** [#2172 — Don't allow any clip in the sequence folder](https://invent.kde.org/multimedia/kdenlive/-/work_items/2172)  
**Merge Request:** [!866](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/866)  
**Responsáveis:** Gustavo Oki e Davi Rodrigues Nunes

---

## Sobre a Sprint 2

Esta sprint foi dedicada ao **acompanhamento do Merge Request !866**, submetido ao repositório oficial do Kdenlive com a correção da issue #2172. O foco principal foi monitorar o processo de revisão pela comunidade, responder a feedbacks dos mantenedores e realizar os ajustes necessários para que o MR atingisse os padrões exigidos para merge.

---

## Entradas do Diário

---

### Entrada 01 — Submissão Formal do MR !866

**Responsáveis:** Gustavo e Davi

Após a conclusão e validação local da solução na Sprint 1, realizamos a submissão formal do Merge Request ao repositório upstream do Kdenlive. O MR foi aberto em **10 de maio de 2026**, a partir do fork de Davi (`davirnunes/kdenlive:master`), com destino ao branch `master` do repositório oficial.

**Detalhes do MR no momento da abertura:**

| Campo | Valor |
|---|---|
| **Título** | Don't allow regular clips in the sequence folder |
| **Autor** | Davi Rodrigues Nunes (`@davirnunes`) |
| **Co-autor** | Gustavo Oki (`@gustoki`) |
| **Branch de origem** | `davirnunes/kdenlive:master` |
| **Branch de destino** | `master` |
| **Commits** | 5 |
| **Arquivos alterados** | 2 |
| **Pipelines** | 2 |

A descrição do MR incluiu uma explicação clara do problema e da abordagem adotada, além da referência explícita à issue:

```
Fixes #2172

I worked on this issue and implemented the restriction to prevent regular
clips from being imported into the sequence folder. Now only sequence clips
are allowed in that folder.

Co-Author: https://invent.kde.org/gustoki
```

---

### Entrada 02 — Acompanhamento Inicial e Pipelines de CI

**Responsável principal:** Gustavo  
**Revisão:** Davi

Logo após a abertura do MR, acompanhamos a execução dos dois pipelines de CI disparados automaticamente pelo GitLab do KDE.

**Pipeline 1 (build básico):** concluiu sem erros de compilação. Os arquivos `projectitemmodel.cpp`, `projectitemmodel.h` e `bin.cpp` compilaram corretamente no ambiente de CI.

**Pipeline 2 (análise estática / clazy):** retornou dois avisos não-bloqueantes relacionados a estilo de código do projeto:

- Uso de `QLatin1Char` onde o projeto prefere literais de string direta em alguns contextos;
- Indentação inconsistente em um bloco `if/else` adicionado em `addItem()`.

Nenhum dos dois avisos causou falha no pipeline, mas anotamos para endereçar preventivamente antes da revisão humana dos mantenedores.

---

### Entrada 03 — Feedback Real do Mantenedor

**Responsável principal:** Davi  
**Revisão:** Gustavo

Após alguns dias da abertura do MR, um mantenedor do Kdenlive deixou uma revisão detalhada. O comentário foi extenso e abriu pontos técnicos relevantes, além de sugestões de evolução para o futuro.

> *"Thanks for this contribution, and sorry for my late review. Is there any reason why you removed the comments in ProjectItemModel? Comments can be helpful when looking into the code.*
>
> *Also, the `Sequences` folder can be renamed, so instead of the `Cannot add clips to the Sequences folder` message, I would suggest to get the real folder name and use `Cannot add clips to the %1 folder`. When doing an internal move, we could also add the clip type, so that it would look like: `Cannot add image clips to the %1 folder`.*
>
> *Finally, it would be nice to make this configurable. Maybe adding an entry in the context menu like `Only allow sequence clips`.*
>
> *Finally, not for this MR, but in a second step, it could be nice to make this approach available in each folder, allowing to limit allowed clip types in each folder. For example a context menu like:*
> *Allowed content: All / Sequence Clips / Video Clips / Audio Clips / Image Clips / Title Clips.*
> *This could be stored in a `filter` property of the `ProjectFolder` class, and a function could be added like `allowsClipType(ClipType)`. Then on insert, we would check if the clip type is allowed..."*

**Análise dos pontos levantados:**

**Ponto 1 — Comentários removidos do `ProjectItemModel`:** durante as refatorações da Sprint 1, alguns comentários explicativos do código original foram inadvertidamente apagados. O mantenedor tem razão em apontar isso: comentários são especialmente importantes em código de modelo de dados como o `ProjectItemModel`, que possui lógica de validação não-trivial.

**Ponto 2 — Nome dinâmico da pasta na mensagem de erro:** a pasta de sequências pode ser renomeada pelo usuário, então usar a string hardcoded `"Sequences folder"` na mensagem é incorreto. A sugestão é usar `i18n("Cannot add clips to the %1 folder", folderName)`, obtendo o nome real via `folderItem->displayName()`.

**Ponto 3 — Tipo do clipe na mensagem de movimentação interna:** ao bloquear um drag interno, seria mais informativo indicar o tipo do clipe sendo rejeitado, por exemplo: `"Cannot add image clips to the %1 folder"`. Isso exige mapear o `ClipType` para uma string legível.

**Ponto 4 — Tornar a restrição configurável (escopo deste MR):** adicionar uma entrada no menu de contexto da pasta tipo `"Only allow sequence clips"` que ligue/desligue a restrição. Seria armazenado como um atributo da pasta no modelo.

**Ponto 5 — Filtro genérico por tipo por pasta (fora do escopo deste MR):** visão de longo prazo do mantenedor para permitir que qualquer pasta tenha restrições de tipo configuráveis, com suporte a múltiplos tipos. Essa sugestão é mais ampla e não precisa ser abordada neste MR.

---

### Entrada 04 — Elaboração da Resposta ao Mantenedor

**Responsáveis:** Gustavo e Davi

Com base na análise do feedback, elaboramos uma resposta para postar na thread do MR. O objetivo foi reconhecer cada ponto, confirmar os ajustes que faremos e delimitar o que fica para um MR futuro.

**Resposta elaborada (a ser postada no MR):**

> *"Thank you for the thorough review! We apologize for the delay in responding.*
>
> *Regarding the removed comments: that was unintentional during our refactoring — we will restore the original comments and add new ones where our logic was introduced.*
>
> *The point about the folder name is a great catch. We will replace the hardcoded string with a dynamic name retrieved via `folderItem->displayName()`, making the message read as `Cannot add %1 clips to the '%2' folder` — where `%1` is the clip type and `%2` is the actual folder name. This handles both the rename case and gives more informative feedback on internal moves.*
>
> *For the configurable restriction via context menu (`Only allow sequence clips`): we think this is a good improvement and are happy to include it in this MR. Our plan is to add a boolean property to `ProjectFolder` (e.g. `m_sequenceOnly`) and toggle it through a new context menu action in `bin.cpp`. The validation in `addItem()` and `dropMimeData()` would then check this flag.*
>
> *Regarding the broader per-folder clip type filter (the `allowsClipType(ClipType)` approach): we fully agree this is the right long-term direction, but given its scope we'd prefer to address it in a follow-up MR to keep this one focused. Would it make sense to open a new issue to track that feature?*
>
> *We will push the updated commits shortly."*

---

### Entrada 05 — Situação Atual do MR

**Responsáveis:** Gustavo e Davi

Ao final desta sprint, o MR **!866** permanece **aberto e em revisão**. O mantenedor deixou um feedback detalhado com pontos a endereçar e a resposta foi elaborada, mas por conta da review feita de forma tardia, isso será feito no início da Sprint 3, junto com os commits de ajuste.

**Status consolidado do MR:**

| Item | Status |
|---|---|
| Pipeline de CI (build) | ✅ Passando |
| Pipeline de CI (análise estática) | ✅ Sem erros bloqueantes |
| Feedback do mantenedor recebido | ✅ Analisado e resposta elaborada |
| Resposta postada no MR | ⏳ A postar na Sprint 3 |
| Ajustes de código | ⏳ A implementar na Sprint 3 |
| Aprovação formal | ⏳ Aguardando |
| Merge | ⏳ Pendente |

Os ajustes identificados são viáveis e bem delimitados. A expectativa é implementá-los, postar a resposta e aguardar uma nova rodada de revisão do mantenedor.

---

## Resumo Técnico da Sprint 2

| Aspecto | Detalhe |
|---|---|
| **Foco da sprint** | Acompanhamento e iteração sobre o MR !866 |
| **MR** | [!866 — Don't allow regular clips in the sequence folder](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/866) |
| **Commits no MR** | 5 (conforme submetido; ajustes pendentes para Sprint 3) |
| **Arquivos modificados** | `src/bin/projectitemmodel.cpp`, `src/bin/projectitemmodel.h`, `src/bin/bin.cpp` |
| **Feedbacks recebidos** | 1 revisão do mantenedor com múltiplos pontos (resposta elaborada) |
| **Pipelines** | 2 (ambos passando) |
| **Status final** | Aberto — aguardando aprovação e merge |

---

## Divisão de Contribuições

| Tarefa | Gustavo | Davi |
|---|---|---|
| Abertura e configuração do MR !866 | ✅ | ✅ |
| Acompanhamento dos pipelines de CI | ✅ | — |
| Análise do feedback do mantenedor | ✅ | ✅ |
| Elaboração da resposta ao mantenedor | ✅ | ✅ |
| Planejamento dos ajustes (próxima sprint) | ✅ | ✅ |
| Monitoramento do status de revisão | ✅ | ✅ |

---

## Plano Pessoal para a Próxima Sprint (Sprint 3)

- [ ] Postar a resposta elaborada na thread do MR !866.
- [ ] Restaurar os comentários removidos do `ProjectItemModel` e adicionar comentários nas novas funções.
- [ ] Implementar nome dinâmico da pasta e tipo do clipe na mensagem de erro.
- [ ] Implementar a opção configurável no menu de contexto da pasta (`Only allow sequence clips`).
- [ ] Propor abertura de nova issue para o filtro genérico por tipo por pasta (sugestão do mantenedor para trabalho futuro).
