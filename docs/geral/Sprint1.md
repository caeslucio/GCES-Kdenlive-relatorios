# Relatório de Contribuição – Sprint 1

**Disciplina:** Gestão de Configuração e Evolução de Software  
**Equipe:** Equipe Kdenlive  
**Comunidade/Projeto de Software Livre:** Kdenlive  
**Período da Sprint:** 22/04/2026 – 11/05/2026  

---

## 1. Resumo da Sprint

A Sprint 1 teve como foco primário a transição do ambiente de setup para contribuições práticas de código no projeto Kdenlive. Vários membros da equipe uniram esforços na identificação, depuração e resolução da **Issue #2172** ("Don't allow any clip in the sequence folder"). O trabalho em conjunto resultou no entendimento profundo da arquitetura do *Project Bin* em C++/Qt e culminou com a submissão do **Merge Request !864** para o repositório oficial do ecossistema KDE.

---

## 2. Objetivos da Sprint

- [x] Identificar issues abertas no repositório oficial adequadas para "First Task".
- [x] Compreender a arquitetura de código necessária para solucionar o problema.
- [x] Desenvolver, depurar e testar a solução localmente.
- [x] Submeter ao menos 1 Merge Request para o repositório oficial do Kdenlive.
- [x] Preencher os diários de bordo individuais com os relatos técnicos.

---

## 3. Entregas Coletivas

| Entrega                             | Status    | Link/Referência                                                                           | Observações                                                |
| ----------------------------------- | --------- | ----------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| **Resolução da Issue #2172**        | Concluído | [Issue #2172 no KDE Invent](https://invent.kde.org/multimedia/kdenlive/-/work_items/2172) | Identificação e análise do bug na pasta de Sequências      |
| **Submissão do Merge Request !864** | Concluído | [MR !864 no KDE Invent](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/864)  | Solução submetida e em fase de revisão pela comunidade KDE |

---

## 4. Entregas Individuais

| Integrante                       | Contribuições                                                                                                                                       | Links (Diário de Bordo)                                                              | Observações |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | ----------- |
| Caetano Santos Lucio             | Manutenção do repositório de documentação, correção de links quebrados do MkDocs, inclusão de indexações pendentes e síntese do relatório coletivo. | [Diário de Bordo](../contribuicoes_individuais/CaetanoLucio-180144979/Sprint1.md)    | Concluído   |
| Davi Rodrigues Nunes             | Primeira implementação do fix, refatoração de código, correção de bugs no fluxo de drop e co-submissão do MR.                                       | [Diário de Bordo](../contribuicoes_individuais/DaviRodrigues - 232014413/sprint1.md) | Concluído   |
| Julia dos Reis Teixeira Massuda  | –                                                                                                                                                   | [Diário de Bordo](../contribuicoes_individuais/JuliaMassuda-231035150/sprint1.md)    | Pendente    |
| João Pedro Rodrigues             | –                                                                                                                                                   | [Diário de Bordo](../contribuicoes_individuais/JoaoRodrigues-231035150/sprint1.md)   | Pendente    |
| Karolina Vieira Barbosa          | –                                                                                                                                                   | [Diário de Bordo](../contribuicoes_individuais/KarolinaVieira-202045820/sprint1.md)  | Pendente    |
| Letícia da Silva Monteiro        | Ante a dificuldade de localização de tarefas de entrada adequadas, foram desenvolvidos e integrados ao repositório os templates de Issue e de Merge Request. A medida visa a padronização das demandas e a otimização da triagem técnica pela comunidade.                                                                                                                                                    | [Diário de Bordo](../contribuicoes_individuais/LeticiaMonteiro-231026859/sprint1.md) | Concluído    |
| Lucas Mendonça Arruda            | Mapeamento de rotas de validação (`slotAddClip` e `dropMimeData`), implementação de feedback visual e documentação do MR.                           | [Diário de Bordo](../contribuicoes_individuais/LucasArruda-231035464/Sprint1.md)     | Concluído   |
| Gustavo Oki de Freitas Rodrigues | Diagnóstico e depuração dos bugs iniciais, documentação dos cenários de reprodução, cobertura de cenários falhos e co-submissão do MR.              | [Diário de Bordo](../contribuicoes_individuais/GustavoOki-231034716/sprint1.md)      | Concluído   |

*(Nota: Alguns diários de bordo listados como "Pendente" ainda não foram criados/enviados para o repositório referentes à Sprint 1)*

---

## 5. Maiores Avanços

**Destaques da Sprint:**

- **Superação da Barreira de Entrada:** Sucesso na transição do estudo teórico do código para a implementação e modificação prática da estrutura interna do Kdenlive.
- **Submissão Oficial:** Criação do Merge Request !864 seguindo os rigorosos padrões de formatação, commit e guidelines de qualidade de código do KDE.
- **Trabalho Colaborativo Eficaz:** Divisão inteligente de escopo (implementação, revisão, depuração e feedback visual) para resolver um problema lógico espalhado por múltiplos componentes da arquitetura.

---

## 6. Maiores Dificuldades

**Principais desafios enfrentados:**

- **Escala da Codebase:** Navegar e entender uma base de código imensa, com arquivos passando de 1.000 linhas, onde a lógica de validação estava distribuída entre `bin.cpp` e `projectitemmodel.cpp`.
- **Ambiguidade das Issues:** A descrição da Issue #2172 era direta mas faltava cenários explícitos de validação (importação, drags externos, internos), o que exigiu que a equipe fizesse um trabalho amplo de rastreio para cobrir todos os *edge cases*.
- **Casting Seguro em C++:** Dificuldade inicial com conversões de ponteiros em tempo de execução no C++ do Qt, gerando bugs silenciosos e crashs que exigiram horas de depuração estrutural.

---

## 7. Lições Aprendidas

- **Resiliência do Código C++:** O valor da tipagem forte e de um sistema de arquitetura robusto quando lidando com manipulação de dados complexos (áudio e vídeo em tempo real).
- **Importância do Fluxo QA:** Definir claramente os testes manuais e cenários de reprodução de bugs antes de tentar alterar o código evitou refatorações dolorosas.
- **Etiqueta Open Source:** A experiência moldou a equipe no que diz respeito ao nível de polimento exigido para submeter uma requisição de código para um projeto utilizado no mundo todo.

---

## 8. Planejamento para a Próxima Sprint (Sprint 2)

- [ ] Acompanhar a revisão do MR !864 pelos mantenedores e aplicar os ajustes de código solicitados (code review).
- [ ] Identificar novas issues disponíveis para os demais membros engajarem.
- [ ] Incentivar as contribuições em código ou de documentação para o resto da equipe.
- [ ] Preencher os relatórios com os progressos subsequentes.
