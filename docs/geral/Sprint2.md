# Relatório de Contribuição – Sprint 2

**Disciplina:** Gestão de Configuração e Evolução de Software  
**Equipe:** Equipe Kdenlive  
**Comunidade/Projeto de Software Livre:** Kdenlive  
**Período da Sprint:** 12/05/2026 – 25/05/2026  

---

## 1. Resumo da Sprint

A Sprint 2 teve como foco primário a resolução de demandas de usabilidade e triagem no ecossistema do Kdenlive. O trabalho concentrou-se na identificação, depuração e resolução do BUG 406887 ("Mover marcadores de clipe diretamente na timeline"), uma pendência aberta desde 2019. O esforço resultou no entendimento prático do framework de interface em QML e na integração de eventos de arrasto com o motor em C++, culminando com a submissão de um novo Merge Request para o repositório oficial do ecossistema KDE e o monitoramento da contribuição anterior.

Em paralelo, a dupla formada por Davi Rodrigues Nunes e Gustavo Oki acompanhou o Merge Request !866 — "Don't allow regular clips in the sequence folder" —, referente à correção da issue #2172 desenvolvida na Sprint 1. A sprint incluiu a verificação dos pipelines de CI, o recebimento de feedback detalhado de um mantenedor do Kdenlive e a elaboração da resposta técnica a ser publicada na thread do MR no início da Sprint 3.

---

## 2. Objetivos da Sprint

- [x] Identificar relatórios de usabilidade abertos pela comunidade no Bugzilla do KDE com a label "junior-jobs".
- [x] Compreender a arquitetura de interface em QML e sua integração de eventos com o motor em C++.
- [x] Desenvolver, depurar e testar localmente o comportamento de arrasto de componentes na linha de tempo.
- [x] Submeter ao menos 1 Merge Request para o repositório oficial do Kdenlive e monitorar a submissão anterior.
- [x] Preencher os diários de bordo individuais com os relatos técnicos da sprint.
---

## 3. Entregas Coletivas

| Entrega                             | Status    | Link/Referência                                                                           | Observações                                                |
| ----------------------------------- | --------- | ----------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| **Resolução do BUG 406887** | Concluído | [BUG 406887 no Bugzilla](https://bugs.kde.org/show_bug.cgi?id=406887)                     | Identificação e correção da falta de arrasto de marcadores |
| **Submissão do Merge Request !880** | Concluído | [MR !880 no KDE Invent](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/880)  | Implementação do arrasto em QML enviada para a Master       |
| **Monitorização do Merge Request !864**| Concluído | [MR !864 no KDE Invent](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/864)  | Acompanhamento e atualização do código da sprint anterior  |
| **Submissão e Monitorização do Merge Request !866** | Concluído | [MR !866 no KDE Invent](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/866) | Correção da issue #2172 (Don't allow regular clips in the sequence folder) submetida por Davi e Gustavo; pipelines de CI verificados e feedback do mantenedor recebido e analisado |

---

## 4. Entregas Individuais

| Integrante                       | Contribuições                                                                                                                                       | Links (Diário de Bordo)                                                              | Observações |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | ----------- |
| Caetano Santos Lucio             |  | [Diário de Bordo](../contribuicoes_individuais/CaetanoLucio-180144979/Sprint2.md)    | Pendente   |
| Davi Rodrigues Nunes             | Submissão do MR !866 ("Don't allow regular clips in the sequence folder") ao repositório oficial do Kdenlive, corrigindo a issue #2172. Acompanhamento dos pipelines de CI, análise do feedback detalhado recebido do mantenedor (restauração de comentários, mensagens dinâmicas com nome da pasta e tipo do clipe, opção configurável no menu de contexto) e elaboração conjunta da resposta técnica a ser publicada na thread do MR. | [Diário de Bordo](../contribuicoes_individuais/DaviRodrigues - 232014413/sprint1.md) | Concluído   |
| Julia dos Reis Teixeira Massuda  | –                                                                                                                                                   | [Diário de Bordo](../contribuicoes_individuais/JuliaMassuda-231035150/sprint2.md)    | Pendente    |
| João Pedro Rodrigues             | –                                                                                                                                                   | [Diário de Bordo](../contribuicoes_individuais/JoaoRodrigues-231035150/sprint2.md)   | Pendente    |
| Karolina Vieira Barbosa          | –                                                                                                                                                   | [Diário de Bordo](../contribuicoes_individuais/KarolinaVieira-202045820/sprint2.md)  | Pendente    |
| Letícia da Silva Monteiro        | Depois da rejeição da submissão inicial por divergências em diretrizes não documentadas, foram realizados estudos de viabilidade técnica para a mitigação de falhas de comunicação no GitLab. A entrega compreende a sistematização dos requisitos de submissão e o planejamento de estratégias para o preenchimento de lacunas informacionais, visando a redução de retrabalho e o aprimoramento do onboarding de novos contribuidores.                                                                                                                                                    | [Diário de Bordo](../contribuicoes_individuais/LeticiaMonteiro-231026859/sprint2.md) | Concluído    |
| Lucas Mendonça Arruda            |     Implementação da Feature que resolve o BUG 406887 do Kdenlive ao implementar o arrasto de marcadores de clipe com o mouse na linha de tempo (QML). Desenvolvida uma lógica de travas para evitar conflitos com cliques comuns e integrados os movimentos ao motor em C++. Por fim, foi feito o acompanhamento do MR anterior e submetida a nova contribuição via GitLab num novo Merge Request.         | [Diário de Bordo](../contribuicoes_individuais/LucasArruda-231035464/Sprint2.md)     | Concluído   |
| Gustavo Oki de Freitas Rodrigues | Monitoramento dos pipelines de CI do MR !866 (build e análise estática), co-análise do feedback do mantenedor e co-elaboração da resposta técnica a ser publicada na thread do MR. O feedback recebido incluiu pontos sobre comentários de código removidos, mensagens de erro com nome dinâmico da pasta, inclusão do tipo do clipe na mensagem de rejeição e sugestão de opção configurável no menu de contexto da pasta. | [Diário de Bordo](../contribuicoes_individuais/GustavoOki-231034716/sprint2.md)      | Concluído   |

*(Nota: Alguns diários de bordo listados como "Pendente" ainda não foram criados/enviados para o repositório referentes à Sprint 2)*

---

## 5. Maiores Avanços

**Destaques da Sprint:**

- **Domínio de Interface Dinâmica:** Sucesso no desenvolvimento e manipulação direta de eventos de toque e mouse.
- **Resolução de Bug Histórico:** Correção de um problema de usabilidade na linha de tempo pendente na comunidade desde 2019 (BUG 406887).
- **Consistência no Fluxo Open Source:** Submissão do Merge Request !880 dentro das diretrizes de commit e rastreamento automatizado exigidos pelo ecossistema KDE.
- **Interação com Mantenedores do KDE:** Recebimento e análise de feedback detalhado de um mantenedor sobre o MR !866, com sugestões técnicas — nome dinâmico da pasta, tipo do clipe na mensagem e opção configurável no menu de contexto — que enriqueceram a solução e abriram caminho para contribuições futuras.

---

## 6. Maiores Dificuldades

**Principais desafios enfrentados:**

- **Mediação e Concorrência de Eventos:** Dificuldade técnica para programar o comportamento do mouse de forma que aceitasse cliques simples, duplos e o arrasto fluido sem gerar conflitos na interface.
- **Ajustes de Sincronia QML/C++:** Desafio em depurar e garantir que a nova coordenada visual calculada em JavaScript/QML atualizasse corretamente os dados estruturais do projeto via C++.
- **Tratamento de Feedback Tardio:** O feedback do mantenedor sobre o MR !866 chegou de forma tardia em relação à abertura do MR, comprimindo o tempo disponível para análise e planejamento dos ajustes dentro da sprint.

---

## 7. Lições Aprendidas

- **Tratamento de Inputs Gráficos:** Aprendizado prático sobre captura, tratamento de coordenadas e filtragem de ruídos em movimentações de mouse (MouseArea).
- **Integração Tecnológica Fluida:** Entendimento real de como o ecossistema do Qt interliga a camada visual (QML) com as regras de negócio em C++.
- **Autonomia em Resolução de Bugs:** Aceleração do aprendizado ao interpretar do zero as queixas de usuários no Bugzilla do KDE e transformá-las em correções de código estáveis.
- **Comunicação Técnica em Projetos Open Source:** Aprendizado sobre como estruturar respostas a revisores da comunidade, equilibrando os ajustes solicitados no escopo atual do MR com sugestões de maior porte encaminhadas para trabalhos futuros.

---

## 8. Planejamento para a Próxima Sprint (Sprint 3)

- [ ] Acompanhar o feedback e realizar possíveis ajustes nos Merge Requests abertos anteriormente conforme as revisões dos mantenedores.
- [ ] Criar uma nova issue no repositório oficial do Kdenlive para a próxima contribuição de código.
- [ ] Registrar o progresso técnico nos diários de bordo individuais e relatórios coletivos.
