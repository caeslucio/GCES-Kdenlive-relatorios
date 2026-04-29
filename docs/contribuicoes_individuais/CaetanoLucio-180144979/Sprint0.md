# Diário de Bordo – Caetano Santos Lucio

**Disciplina:** Gestão da Configuração e Evolução de Software (GCES)  
**Equipe:** GCES 2026.1 – Kdenlive  
**Comunidade/Projeto de Software Livre:** [Kdenlive](https://invent.kde.org/multimedia/kdenlive)  
**Matrícula:** 180144979  
**GitHub:** [@caeslucio](https://github.com/caeslucio)  
**KDE Invent:** [@caeslucio](https://invent.kde.org/caeslucio)

---

## Sprint 0 – 01/04/2026 – 21/04/2026

### Resumo da Sprint

Sprint 0 foi dedicada à consolidação da arquitetura de base do projeto. As atividades focaram na validação inicial da engenharia de documentação do grupo utilizando o MkDocs Material, incluindo a otimização de UI/UX, baseada no repositório GCES-OPPIA. Paralelamente, o ambiente pessoal de desenvolvimento foi configurado: as regras de submissão da comunidade KDE foram validadas, os acessos credenciados ao KDE Invent oficial foram obtidos, e a base original do Kdenlive foi clonada localmente, estabelecendo os alicerces para o início do desenvolvimento nas próximas Sprints.

---

### Atividades Realizadas

| Data  | Atividade                                                                           | Tipo   | Link/Referência                                                                   | Status    |
| ----- | ----------------------------------------------------------------------------------- | ------ | --------------------------------------------------------------------------------- | --------- |
| 13/04 | Análise do repositório modelo (GCES-OPPIA-relatorios)                               | Estudo | [GCES-OPPIA-relatorios](https://github.com/LuizaMaluf/GCES-OPPIA-relatorios)      | Concluído |
| 13/04 | Criação da estrutura de pastas do novo repositório                                  | Doc    | [GCES-Kdenlive-relatorios](https://github.com/caeslucio/GCES-Kdenlive-relatorios) | Concluído |
| 13/04 | Estruturação inicial do repositório, configuração do CI/CD e criação de templates   | Doc    | Vários arquivos                                                                   | Concluído |
| 14/04 | Preenchimento inicial de diários e formulação dos guias de contribuição             | Doc    | [materiais/](../../materiais/como-abrir-mr.md)                                    | Concluído |
| 17/04 | Estudo de regras de contribuição, registro de conta KDE e clone do repositório base | Dev    | Repositório local e KDE Invent                                                    | Concluído |
| 21/04 | Refatoração estrutural do MkDocs, revisão de conectividade e aprimoramento UI/UX    | Dev/QA | Vários arquivos                                                                   | Concluído |

---

### Maiores Avanços

- **Infraestrutura de documentação completa**: o repositório foi criado com estrutura MkDocs Material, menu de navegação configurado, modo escuro/claro, busca integrada e CI/CD funcional.
- **Configuração do Ambiente de Trabalho**: Testada a infraestrutura para esta Sprint. Código fonte do Kdenlive clonado e configurado na estação local.
- **Guias de contribuição**: Guias de abertura e regras de MR escritos com base na documentação oficial do Kdenlive. O projeto usa o KDE GitLab (`invent.kde.org`), o Bugzilla do KDE para rastreamento de bugs e requer conta KDE Identity.
- **Pesquisa do ecossistema KDE**: Entendimento de como funciona o fluxo de contribuição da KDE — criação de conta no [identity.kde.org](https://identity.kde.org), fork no GitLab, abertura de Merge Requests, uso do Bugzilla como rastreador de bugs e do fórum [discuss.kde.org](https://discuss.kde.org/tag/kdenlive) como canal de comunicação.

---

### Maiores Dificuldades

- **Volume de Estruturação Inicial**: A montagem de uma arquitetura central, capaz de consolidar com precisão as tabelas, guias e o alto volume de dados técnicos necessários para o início do projeto reduziu nossa margem de prazos locais.

!!! warning "Nota de Responsabilidade"
    Como arquiteto da documentação, assumo inteiramente a responsabilidade pela incompletude dos logs, tabelas de membros e diários individuais da equipe nesta entrega. A equipe não teve tempo hábil para preencher seus dados, pois só liberei e passei as instruções de uso do repositório no próprio dia do encerramento da Sprint. Os membros que não conseguiram entregar suas métricas a tempo não devem ser prejudicados na avaliação por essa restrição técnica, que será devidamente reparada nas próximas *releases* da documentação.

---

### Aprendizados

- O ecossistema KDE tem sua própria infraestrutura de identidade (`identity.kde.org`) e rastreamento de bugs (`bugs.kde.org/bugzilla`), separada do GitHub/GitLab público.
- No Kdenlive, as contribuições de código acontecem via **Merge Requests** no [invent.kde.org](https://invent.kde.org/multimedia/kdenlive), seguindo o **KDE Coding Style** para C++ e QML.

---

### Plano Pessoal para a Próxima Sprint (Sprint 1)

- [ ] Identificar ao menos 1 issue ou bug aberto no [Bugzilla do KDE](https://bugs.kde.org/buglist.cgi?product=kdenlive&resolution=---) para trabalhar.
- [ ] Abrir ou comentar em ao menos 1 issue ou MR no repositório oficial.
- [ ] Escrever o diário de bordo da Sprint 1.
