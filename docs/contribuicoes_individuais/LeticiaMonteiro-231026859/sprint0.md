# Relatório de Contribuição – Sprint 0
 
Disciplina: Gestão de Configuração e Evolução de Software  
Equipe: GCES 2026.1 – Kdenlive  
Comunidade/Projeto: KDE / Kdenlive  
Matrícula: 231026859  
GitHub: @LeticiaMonteiroo  
KDE Invent: @leticia
Período: 13/04/2026 – 21/04/2026
 
---
 
## 1. Resumo da Sprint

A Sprint 0 teve como foco a imersão no ecossistema do projeto Kdenlive e na preparação do ambiente de desenvolvimento. Inicialmente, foram realizadas tentativas de configuração no Windows, incluindo uso do Git Bash e análise da documentação oficial do projeto.  

Devido à complexidade das dependências (Qt6, KDE Frameworks 6 e MLT), foi necessário migrar a estratégia para utilização do WSL (Windows Subsystem for Linux). Durante esse processo, houve dificuldades com compatibilidade de versões no Ubuntu, levando à decisão de utilizar uma distribuição mais atualizada.  

Ao final, foi configurado um ambiente utilizando Arch Linux dentro do WSL, permitindo maior controle sobre versões de pacotes e compatibilidade com os requisitos mais recentes do Kdenlive. Também foi realizado o estudo da documentação oficial de build, entendimento das dependências críticas e preparação do ambiente para compilação do projeto.
 
---
 
## 2. Objetivos da Sprint
 
- Padronização: Criar um repositório de relatórios com CI/CD funcional e documentação estruturada.
- Acreditação: Obter credenciais no KDE Identity e acesso ao KDE Invent.
- Configuração de Ambiente: Construir ambiente de desenvolvimento compatível com Qt6, KDE Frameworks 6 e MLT utilizando WSL.
- Mapeamento: Entender requisitos técnicos de build e regras de contribuição do projeto.
 
---
 
## 3. Entregas Coletivas
 
| Entrega | Status | Link/Referência | Observações |
| :--- | :--- | :--- | :--- |
| Portal MkDocs | Concluído | [Link do Repo/Pages] | Estrutura com navegação, busca e organização dos relatórios. |
| Fork & Clone | Concluído | invent.kde.org/gustoki/kdenlive | Repositório sincronizado localmente. |
| Guia de Contribuição | Concluído | /materiais/guia_contribuicao.md | Baseado nas diretrizes oficiais do projeto. |
 
---
 
## 4. Log de Atividades
 
| Data | Atividade | Tipo | Status |
| :--- | :--- | :--- | :--- |
| 15/04 | Estudo inicial da arquitetura do projeto Kdenlive | Estudo |  |
| 16/04 | Criação de conta no KDE Identity | Outro |  |
| 17/04 | Setup do MkDocs Material e CI/CD | Doc/Infra |  |
| 18/04 | Tentativa de configuração via Git Bash no Windows | Ambiente |  |
| 19/04 | Estudo da documentação oficial de build (Qt6, KF6, MLT) | Estudo |  |
| 20/04 | Configuração do WSL e testes com Ubuntu | Ambiente |  |
| 21/04 | Migração para Arch Linux no WSL e instalação de dependências | Ambiente |  |
 
---
 
## 5. Maiores Avanços
 
- Compreensão do ecossistema KDE: entendimento das dependências modernas como Qt6, KDE Frameworks 6 e MLT.
- Adaptação de ambiente: migração de Windows puro para WSL e posteriormente para Arch Linux, garantindo compatibilidade com o projeto.
- Leitura e interpretação de documentação técnica: capacidade de seguir e adaptar guias oficiais complexos de build.
- Estrutura de projeto open source: entendimento inicial do fluxo de contribuição e organização do código.
 
---
 
## 6. Maiores Dificuldades

- Compatibilidade de dependências: conflitos entre versões (especialmente ECM/KF5 vs KF6).
- Ambiente Windows: limitações do Git Bash e dificuldade de build nativo.
- Configuração do WSL: necessidade de entender a separação entre ambiente Windows e Linux.
- Complexidade do build: grande quantidade de bibliotecas e dependências externas.
 
---
 
## 7. Lições Aprendidas
 
- Gestão de Ambiente: projetos grandes exigem alinhamento exato de versões de dependências.
- Escolha de ferramentas: nem sempre a solução mais “fácil” (como Docker ou Craft) é a melhor para desenvolvimento real.
- WSL como solução híbrida: permite usar Linux mantendo o Windows, sendo essencial para desenvolvimento em projetos open source complexos.
- Documentação técnica: saber interpretar documentação oficial é uma habilidade crítica.
 
---
 
## 8.