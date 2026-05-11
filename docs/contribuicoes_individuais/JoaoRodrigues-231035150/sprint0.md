# Diário de Bordo – João Pedro

**Disciplina:** Gestão da Configuração e Evolução de Software (GCES)  
**Equipe:** GCES 2026.1 – Kdenlive  
**Comunidade/Projeto de Software Livre:** [Kdenlive](https://invent.kde.org/multimedia/kdenlive)  
**Matrícula:** 231026966  **GitHub:** [@joaopedro](https://github.com/JpRodrigues2)  **KDE Invent:** [@joaorodrigues](https://invent.kde.org/joaorodrigues)

---

## Sprint 0 – 01/04/2026 – 21/04/2026

### 1. Resumo da Sprint
A Sprint 0 foi focada no *onboarding* técnico e na preparação da infraestrutura de desenvolvimento. O objetivo principal foi superar a barreira de entrada do ecossistema KDE, que possui ferramentas e fluxos de trabalho específicos (KDE Identity e Invent). Realizei a configuração do ambiente local em ambiente Unix, focando na compilação das dependências necessárias para o Kdenlive e na integração com o pipeline de documentação da equipe via MkDocs.

---

### 2. Atividades Realizadas

| Data | Atividade | Tipo | Link/Referência | Status |
| :--- | :--- | :--- | :--- | :--- |
| 14/04 | Estudo do fluxo de trabalho Gitlab (KDE Invent) vs GitHub | Estudo | [KDE Wiki](https://community.kde.org/Infrastructure/GitLab) | Concluído |
| 15/04 | Criação e validação da conta no KDE Identity | Infra | [Identity KDE](https://identity.kde.org/) | Concluído |
| 16/04 | Fork do repositório Kdenlive e configuração de chaves SSH | Dev | [Kdenlive Invent](https://invent.kde.org/multimedia/kdenlive) | Concluído |
| 18/04 | Setup do ambiente de build (CMake/Qt5) e resolução de dependências | Ambiente | Repositório Local | Concluído |
| 20/04 | Contribuição na estrutura inicial do portal de documentação | Doc | MkDocs / GitHub Pages | Concluído |

---

### 3. Maiores Avanços

- **Interoperabilidade de Ferramentas:** Sucesso na integração do fluxo de trabalho local com as exigências da comunidade KDE, garantindo que o ambiente de desenvolvimento esteja pronto para submissão de código.
- **Automação de Documentação:** Colaborei na configuração do CI/CD para o MkDocs, assegurando que o progresso técnico da equipe seja refletido em tempo real no portal de relatórios.
- **Compilação Local:** Concluí o processo de build do projeto, um passo crítico dado a complexidade das dependências de áudio e vídeo do Kdenlive.

---

### 4. Maiores Dificuldades

- **Gerenciamento de Dependências:** A configuração inicial exigiu a resolução manual de conflitos de bibliotecas de sistema, especialmente relacionadas aos frameworks do Qt e MLT, o que demandou um tempo considerável de pesquisa técnica.
- **Curva de Aprendizado da Infra KDE:** Compreender a separação entre o Bugzilla para rastreamento e o Invent para versionamento exigiu uma adaptação em relação ao fluxo centralizado do GitHub.

---

### 5. Lições Aprendidas

- **Cultura de Desenvolvimento KDE:** Aprendi que a comunicação via canais oficiais (Matrix e Fóruns) é fundamental antes de iniciar qualquer implementação complexa para evitar retrabalho.
- **Modularidade C++/Qt:** Pude observar a organização modular do código fonte do Kdenlive, o que facilitará a identificação de pontos de melhoria nas próximas sprints.

---

### 6. Plano Pessoal para a Próxima Sprint (Sprint 1)

- [ ] Realizar o mapeamento de classes principais relacionadas à interface de usuário (QML).
- [ ] Localizar e analisar uma "Good First Issue" no Bugzilla do KDE para propor um Merge Request inicial.
- [ ] Documentar o fluxo de testes unitários do projeto para auxiliar o restante da equipe.
