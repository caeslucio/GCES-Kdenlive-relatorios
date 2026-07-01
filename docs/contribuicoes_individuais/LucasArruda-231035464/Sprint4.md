# Diário de Bordo – Lucas

**Disciplina:** GERÊNCIA DE CONFIGURAÇÃO E EVOLUÇÃO DE SOFTWARE  
**Equipe:** GCES 2026.1 – Kdenlive  
**Comunidade/Projeto de Software Livre:** [Kdenlive](https://invent.kde.org/multimedia/kdenlive)  
**Sprint:** Sprint 4 (08/06/2026 – 30/06/2026)  
**Matrícula:** 231035464   
**GitHub:** [@lucasarruda](https://github.com/lucasarruda9)  
**KDE Invent:** [@lucasma](https://invent.kde.org/lucasma)

---

## 1. Resumo da Sprint 4 (08/06/2026 - 30/06/2026)

A Sprint 4 foi focada na evolução e refinamento do Merge Request iniciado nas sprints anteriores para o Kdenlive (**BUG 406887**). Após implementar a funcionalidade base de arrasto de marcadores de clipe (Sprint 2) e o suporte ao sistema de histórico Undo/Redo (Sprint 3), o trabalho nesta sprint concentrou-se em reestruturar completamente a abordagem técnica com base no feedback arquitetural dos mantenedores.

### 1.1 Acompanhamento e Feedback do MR #880

Dando continuidade ao acompanhamento do Merge Request #880, o mantenedor Jean forneceu um feedback a respeito das limitações da abordagem anterior. Embora o sistema de Undo/Redo desenvolvido na Sprint 3 estivesse funcionando bem, ele pontuou que o uso do arrasto nativo do QML (`Drag`) impedia a implementação correta da mecânica de *snapping*, que é a atração magnética aos pontos de referência da Timeline.

Para solucionar o problema, Jean propôs uma mudança de arquitetura inspirada no funcionamento dos marcadores da régua principal (`Ruler.qml`), fornecendo uma prova de conceito em formato de patch. A orientação consistia em trocar o componente de arrasto por manipulação manual de coordenadas e dividir o movimento do marcador em duas etapas no backend para não entupir a pilha de histórico do usuário.

![Feedback dos Mantenedores no GitLab](../../assets/contribuicoes_individuais/lucas/sprint3/feedback.png)
*Figura 1: Discussão técnica com os mantenedores do Kdenlive*

### 1.2 Resolução de Conflitos e Ajustes no Linter

Durante a integração do patch e testes no pipeline de Integração Contínua (CI) do GitLab, a build falhou devido a restrições estritas do linter de QML do projeto (`all_qmllint`). O validador acusou problemas de "Unqualified access" no arquivo `Clip.qml`, identificando trechos de código legados anteriores à alteração que passaram a ser validados pelo escopo do linter devido à nova edição. Esse comportamento gerava um erro fatal na pipeline e travava a compilação local, impedindo os testes da nova funcionalidade.

Para mitigar o problema e destravar o fluxo de desenvolvimento em ambiente local, foi necessário remover temporariamente a dependência `add_dependencies(kdenlive all_qmllint)` na linha 369 do arquivo `CMakeLists.txt` (localizado no diretório `src`). Essa alteração foi mantida estritamente fora dos commits para não modificar as regras globais do projeto. Por fim, para garantir a conformidade com a esteira do GitLab, o escopo das variáveis foi devidamente qualificado e ajustado dentro das frentes de trabalho afetadas no arquivo QML, resolvendo os avisos e liberando o pipeline.

### 1.3 Descrição da Nova Demanda (Evolução Técnica)

A nova especificação exigiu a substituição do arrasto baseado em componentes nativos de `Drag` pelo controle manual de fluxo de coordenadas e eventos de mouse. O objetivo principal consistiu em:

* **Gerenciamento de Eventos Visuais (`WithoutUndo`):** Implementar e invocar o método `moveClipMarkerWithoutUndo` no C++ para atualizar a posição visual do marcador dinamicamente no evento `onPositionChanged` do QML.
* **Transação Definitiva (`moveClipMarker`):** No evento `onReleased`, restaurar momentaneamente o marcador à posição original do clique e aplicar o movimento definitivo associado à pilha de Undo/Redo do `pCore`, garantindo um histórico limpo e o funcionamento perfeito do Ctrl+Z.
* **Mecânica de Snapping:** Integrar a função de cálculo de quadros (`suggestSnapPoint`) para que o marcador seja atraído magneticamente pelos cortes e referências da timeline ao ser arrastado.

### 1.4 Contribuição

O desenvolvimento desta sprint estruturou-se nas seguintes frentes:

* **Backend:** Criação e declaração do método `moveClipMarkerWithoutUndo` na classe `TimelineController`, tratando travas de concorrência com `QMutexLocker`, validação de limites com `qBound` e acesso direto ao modelo de dados do clipe binário (`markerModel->moveMarker`).
* **Frontend com QML** Refatoração do bloco `markerComponent` no arquivo `Clip.qml`. Foi implementada  o mapeamento de coordenadas com `mapToItem`, o cálculo de deltas em frames proporcionais ao zoom/velocidade da linha de tempo e as lógicas de disparo sequencial nos estados `onPressed`, `onPositionChanged` e `onReleased`.

### 1.5 Atualização do Merge Request

As modificações de refatoração estrutural foram commitadas atualizando o merge request. O histórico manteve-se indexado à issue original (`BUG: 406887`) para fins de rastreabilidade de código e evolução de software.

![Merge Request da contribuição atualizado](../../assets/contribuicoes_individuais/lucas/sprint4/contribuicao_atualizada.png)
*Figura 2: Histórico de modificações atualizado no Merge Request #880*

---

## 2. Atividades Realizadas

| Data  | Atividade | Tipo | Referência | Status    |
| ----- | --------- | ---- | ---------- | --------- |
| 10/06/2026 | Analisar a proposta de arquitetura de movimento enviada pelo mantenedor Jean | Estudo | [Link](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/880) | Concluído |
| 15/06/2026 | Mapear o comportamento e funções de snapping implementadas no `Ruler.qml` | Estudo | [Link](https://invent.kde.org/lucasma/kdenlive/-/blob/feat/move-clip-marker-with-mouse/src/timeline2/view/qml/Ruler.qml?ref_type=heads) | Concluído |
| 21/06/2026 | Implementar o método C++ `moveClipMarkerWithoutUndo` no `TimelineController` | Código | [Link](https://invent.kde.org/lucasma/kdenlive/-/commit/57b2d7f1b55111616023834541ef6351d97f0f73) | Concluído |
| 22/06/2026 | Refatorar a captura de eventos de mouse e cálculo de deltas de frames no `Clip.qml` | Código | [Link](https://invent.kde.org/lucasma/kdenlive/-/commit/57b2d7f1b55111616023834541ef6351d97f0f73) | Concluído |
| 25/06/2026 | Integrar a mecânica de `suggestSnapPoint` ao fluxo de arrasto dos marcadores de clipe | Código | [Link](https://invent.kde.org/lucasma/kdenlive/-/commit/57b2d7f1b55111616023834541ef6351d97f0f73) | Concluído |
| 28/06/2026 | Commitar alterações para o Merge Request | Código | [Link](https://invent.kde.org/lucasma/kdenlive/-/commit/57b2d7f1b55111616023834541ef6351d97f0f73) | Concluído |
| 30/06/2026 | Documentar diário de bordo da Sprint 4 | Documentação | [Link](https://github.com/caeslucio/GCES-Kdenlive-relatorios) | Concluído |

---

## 3. Maiores Avanços

* **Cálculo de Snapping na Timeline:** Sucesso na implementação da mecânica para fazer o marcador alinhar-se ("grudar") aos pontos de referência da linha de tempo. Para isso, foi necessário converter a posição do mouse em pixels para quadros (frames) exatos do vídeo, considerando o nível de zoom atual e a taxa de FPS do projeto.

* **Resolução de Problemas com Linters Estritos:** Compreensão do funcionamento e depuração do `qmllint` da KDE, que bloqueava a compilação por conta de escopos de variáveis não qualificados (`Unqualified access`). A resolução desse problema trouxe maior domínio sobre como o projeto organiza e valida o escopo de seus componentes QML.

---

## 4. Histórico de Versões

| Versão | Descrição                                                      | Autor(es)                            | Data       | 
|--------|----------------------------------------------------------------|--------------------------------------|------------|
| 1.0    | Adiciona seção de resumo da sprint 4 | [Lucas Mendonça](https://github.com/lucasarruda9) | 30/06/2026 |
| 1.1    | Adiciona seção de atividades realizadas e maiores avanços | [Lucas Mendonça](https://github.com/lucasarruda9) | 30/06/2026 |