# Diário de Bordo – Caetano Santos Lucio

**Disciplina:** Gestão da Configuração e Evolução de Software (GCES)  
**Equipe:** GCES 2026.1 – Kdenlive  
**Comunidade/Projeto de Software Livre:** [Kdenlive](https://invent.kde.org/multimedia/kdenlive)  
**Matrícula:** 180144979  
**GitHub:** [@caeslucio](https://github.com/caeslucio)  
**KDE Invent:** [@caeslucio](https://invent.kde.org/caeslucio)

---

## Sprint 1 – 22/04/2026 – 11/05/2026

### 1. Resumo da Sprint

Nesta Sprint, atuei como mantenedor e facilitador do repositório da equipe, garantindo a integridade, organização e a escalabilidade da base de conhecimento gerada para a Sprint 1. Minha contribuição se concentrou na revisão de links quebrados e correções arquiteturais do portal web no MkDocs, na atualização da árvore do menu de navegação e na síntese técnica de todas as informações geradas pela equipe no Relatório Geral da Sprint 1, integrando o trabalho prático (resolução da issue #2172) do Lucas, Gustavo e Davi em uma documentação coletiva e padronizada.

---

### 2. Atividades Realizadas

| Data | Atividade | Tipo | Referência | Status |
| :--- | :--- | :--- | :--- | :--- |
| 29/04 | Varredura de links fantasmas do MkDocs e revisão dos diretórios baseados em templates  | Infra / Doc | Vários arquivos e repositório local | Concluído |
| 29/04 | Configuração de UI/UX do portal de documentação (remoção de expansão automática de menus laterais) | Dev / Infra | `mkdocs.yml` | Concluído |
| 29/04 | Revisão e validação de hyper-links do GitLab (KDE Invent) e GitHub de todos os membros | Doc | Vários diários de bordo | Concluído |
| 11/05 | Identificação e inclusão de diários não mapeados no pipeline do MkDocs (`sprint1.md` e `sprint0.md`) | Infra | `mkdocs.yml` | Concluído |
| 11/05 | Síntese, coleta de dados cruzada e produção do Relatório Geral Coletivo da Sprint 1 | Doc | `docs/geral/Sprint1.md` | Concluído |
| 11/05 | Documentação do diário de bordo e submissão dos rastreios de gestão da Sprint 1 | Doc | `CaetanoLucio-180144979/Sprint1.md` | Concluído |

---

### 3. Maiores Avanços

- **Gerenciamento de Integração Contínua em Doc:** Consolidação do ecossistema do MkDocs. Assegurei de que qualquer inconsistência proveniente do template copiado por outros membros fosse reestruturada para não comprometer o build automatizado.
- **Produção e Síntese de Relatório Coletivo:** Compilação dos desafios e implementações técnicas em código C++/Qt feitos pela equipe na resolução de bugs (MR #864), adequando essa estrutura para o portal acadêmico exigido na Sprint 1.

---

### 4. Maiores Dificuldades

- Lidar com dependências textuais que haviam ficado para trás após a configuração da Sprint 0. Exigiu múltiplas validações para estancar os "warnings" gerados pelo pipeline em links falsos.
- Realizar a triangulação de leitura dos relatos de vários membros (Davi, Gustavo e Lucas) que realizaram um trabalho cruzado numa mesma demanda técnica.

---

### 5. Lições Aprendidas

- O poder das manutenções passivas de repositórios: ter ferramentas (como o output do MkDocs local) avisando os erros imediatamente facilita encontrar inconsistências na entrega da equipe.
- Ao compilar dados de documentações colaborativas, a padronização e o uso rígido de templates se provam essenciais.

---

### 6. Plano Pessoal para a Próxima Sprint (Sprint 2)

- [ ] Mergulhar ativamente na análise do C++/Qt para resolver uma "Good First Issue" no KDE Invent em formato de par ou individualmente.
- [ ] Submeter um Merge Request contribuindo para a evolução do software base.
- [ ] Manter a fiscalização da documentação gerada pelo resto da equipe na aba coletiva.
