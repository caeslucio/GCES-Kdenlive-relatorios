# Relatório de Contribuição – Sprint 3

**Disciplina:** Gestão de Configuração e Evolução de Software  
**Equipe:** Equipe Kdenlive  
**Comunidade/Projeto de Software Livre:** Kdenlive  
**Período da Sprint:** 26/05/2026 – 08/06/2026  

---

## 1. Resumo da Sprint

A Sprint 3 foi focada na resolução de problemas de usabilidade, evolução de recursos e refinamento de contribuições anteriores para o Kdenlive, dividindo-se em duas grandes frentes de trabalho:

1. **Evolução Técnica do Recurso de Marcadores (BUG 406887):** Diante dos feedbacks dos mantenedores no Merge Request #880, o escopo foi expandido para mitigar interações acidentais na linha de tempo. Foi implementado o suporte transacional completo a comandos de desfazer e refazer (Undo/Redo) para o movimento de marcadores de Clipe via interface QML e engine C++.
2. **Correção na Exportação de WebP Animado (BUG 508117):** Identificação e correção do bug que impedia usuários de configurar o número de loops diretamente pela interface do Kdenlive ao exportar arquivos WebP, culminando na abertura do Merge Request !891.

Em paralelo, a equipe manteve o acompanhamento de contribuições passadas, realizando rebase de branches e publicando atualizações na thread do MR !866.

---

## 2. Objetivos da Sprint

- [x] Implementar o suporte completo a Undo/Redo para movimentação de marcadores de clipe (MR #880).
- [x] Resolver conflitos de código através de Git Rebase com a branch `master` upstream no MR #880.
- [x] Identificar e analisar o BUG 508117 no Bugzilla do KDE.
- [x] Implementar o campo "Loop Count" na interface de edição de presets de renderização do Kdenlive.
- [x] Adicionar o preset "WebP Animation" na categoria "Images sequence" do repositório de presets.
- [x] Testar localmente as soluções e validar os parâmetros gerados nos arquivos finais.
- [x] Submeter/atualizar os Merge Requests correspondentes no repositório oficial do Kdenlive.

---

## 3. Entregas Coletivas

| Entrega | Status | Link/Referência | Observações |
| ------- | ------ | --------------- | ----------- |
| **Evolução do MR #880 (Undo/Redo)** | Concluído | [MR #880 no KDE Invent](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/880) | Integração para movimentação de marcadores de clipes |
| **Resolução do BUG 508117** | Concluído | [BUG 508117 no Bugzilla](https://bugs.kde.org/show_bug.cgi?id=508117) | Adição do campo Loop Count para WebP animado |
| **Submissão do Merge Request !891** | Concluído | [MR !891 no KDE Invent](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/891) | Implementação do Loop Count no editor de presets |
| **Resposta ao mantenedor do MR !866** | Concluído | [MR !866 no KDE Invent](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/866) | Resposta publicada com plano de ajustes |

---

## 4. Entregas Individuais

| Integrante | Contribuições | Links (Diário de Bordo) | Observações |
| ---------- | ------------- | ----------------------- | ----------- |
| Caetano Santos Lucio | – | [Diário de Bordo](../contribuicoes_individuais/CaetanoLucio-180144979/Sprint3.md) | Pendente |
| Davi Rodrigues Nunes | Análise da issue e do comportamento do parâmetro `loop` no muxer WebP via FFmpeg e MLT. Investigação do bug onde o parâmetro `loop=0` não era incluído nos params por estar dentro de um bloco `if (gopSpinner->value() > 0)`. Participação na implementação e nos testes de validação com `webpmux`. Co-autoria no commit submetido. | [Diário de Bordo](../contribuicoes_individuais/DaviRodrigues-232014413/sprint3.md) | Concluído |
| Gustavo Oki de Freitas Rodrigues | Implementação das modificações nos 3 arquivos do projeto (`editrenderpreset_ui.ui`, `renderpresetdialog.cpp`, `renderpresetrepository.cpp`). Investigação e resolução do bug do parâmetro `loop` não sendo gerado. Testes locais com `webpmux` para validação do `Loop Count: 0`. Submissão e documentação do MR !891. | [Diário de Bordo](../contribuicoes_individuais/GustavoOki-231034716/sprint3.md) | Concluído |
| Julia dos Reis Teixeira Massuda | – | [Diário de Bordo](../contribuicoes_individuais/JuliaMassuda-231035150/sprint2.md) | Pendente |
| João Pedro Rodrigues | – | [Diário de Bordo](../contribuicoes_individuais/JoaoRodrigues-231035150/sprint2.md) | Pendente |
| Karolina Vieira Barbosa | – | [Diário de Bordo](../contribuicoes_individuais/KarolinaVieira-202045820/sprint2.md) | Pendente |
| Letícia da Silva Monteiro | – | [Diário de Bordo](../contribuicoes_individuais/LeticiaMonteiro-231026859/sprint2.md) | Pendente |
| **Lucas Mendonça Arruda** | Resolução de conflitos via Git Rebase no arquivo `Clip.qml` com a master upstream. Criação da função de controle `TimelineController::moveClipMarker` no C++ mapeada como `Q_INVOKABLE` com tratamento transacional (`pCore->pushUndo`). Refatoração da interface QML para substituição do método antigo de arrasto de marcadores de clipe, vinculando o evento ao histórico nativo de Undo/Redo do software. | [Diário de Bordo](../contribuicoes_individuais/LucasArruda-231035464/Sprint3.md) | **Concluído** |

---

## 5. Maiores Avanços

- **Gestão de Transações e Histórico (Command Pattern):** Entendimento prático de como funciona a estrutura de histórico (Undo/Redo) em softwares complexos de edição de vídeo, acoplando a interface gráfica (QML) com pilhas de ações em C++ de forma segura.
- **Evolução de Software Baseada em Code Review:** Vivência real do ciclo de vida de uma contribuição open-source, adaptando componentes de interface e regras de negócio a partir do feedback direto dos mantenedores do Kdenlive.
- **Resolução de problema real de usabilidade em renderização:** Eliminação da necessidade de executar comandos manuais via terminal (`webpmux`) pós-exportação de WebP animado.
- **Integração profunda com o pipeline MLT/FFmpeg:** Compreensão de como propriedades de componentes de interface se traduzem em AVOptions dentro do motor de renderização do ecossistema KDE.

---

## 6. Maiores Dificuldades

- **Gerenciamento de Contexto no Histórico do Core:** Compreender e depurar o fluxo do `markerModel->moveMarkers` em conjunto com o barramento do `pCore`, garantindo que as referências de desfazer e refazer funcionassem sem corromper o modelo de dados da timeline.
- **Bug silencioso do bloco GOP:** Identificação de que o parâmetro `loop=0` para o WebP estava sendo omitido por estar erroneamente aninhado dentro de uma condicional de verificação do GOP.
- **Ambiente de Testes Local Limitado:** O FFmpeg distribuído pelo ambiente padrão do KDE Craft veio sem suporte nativo à `libwebp_anim`, exigindo substituição manual de bibliotecas dinâmicas (DLLs) para homologação do código.

---

## 7. Lições Aprendidas

- **Robustez em Interfaces Gráficas:** Funcionalidades de manipulação direta (como o arrasto por mouse) exigem mechanisms transacionais acoplados ao motor de dados para garantir a integridade do estado da aplicação.
- **Comunicação com Camadas de Abstração:** O MLT repassa opções ao FFmpeg de forma proprietária, agindo como propriedades do consumer `avformat`, demandando mapeamento rigoroso de nomenclatura.
- **Análise Incremental de Causa Raiz:** A importância de debugar o fluxo de dados em camadas (Interface -> Preset Salvo -> Script MLT -> Arquivo Binário Gerado) para isolar falhas de integração.

---

## 8. Planejamento para a Próxima Sprint (Sprint 4)

- [ ] Acompanhar a avaliação final e feedbacks dos mantenedores nos MRs !891 e #880.
- [ ] Realizar eventuais ajustes pontuais ou refatorações solicitadas pela comunidade do Kdenlive nos patches submetidos.
- [ ] Implementar os ajustes planejados para o MR !866 (nome dinâmico da pasta, tipo do clipe e menus de contexto).
- [ ] Mapear novas issues e bugs abertos no Bugzilla para iniciar novas frentes de contribuição.
- [ ] Registrar o progresso nos diários de bordo individuais da Sprint 4.
