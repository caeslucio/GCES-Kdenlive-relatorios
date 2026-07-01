# Relatório de Contribuição – Sprint 4

**Disciplina:** Gestão de Configuração e Evolução de Software  
**Equipe:** Equipe Kdenlive  
**Comunidade/Projeto de Software Livre:** Kdenlive  
**Período da Sprint:** 09/06/2026 – 30/06/2026  

---

## 1. Resumo da Sprint

A Sprint 4 concentrou-se no refinamento e na adaptação de contribuições anteriores para o ecossistema do Kdenlive, com base nos retornos da comunidade. O trabalho dividiu-se na seguinte frente principal:

1. **Evolução da Timeline e Sistema de Snapping (BUG 406887):** Substituição do mecanismo de arrasto de marcadores para atender a requisitos arquiteturais dos mantenedores. A alteração permitiu integrar o movimento fluido da interface gráfica com o sistema de atração magnética por quadros (snapping), preparando o Merge Request #880 para a branch principal.

---

## 2. Objetivos da Sprint

- [x] Reformular o mecanismo de arrasto dos marcadores para permitir o alinhamento magnético na timeline.
- [x] Ajustar o tratamento de eventos no código para separar as atualizações visuais da interface do registro histórico de Undo/Redo.
- [x] Validar o comportamento final das alterações diretamente no ambiente oficial do Kdenlive.

---

## 3. Entregas Coletivas

| Entrega | Status | Link/Referência | Observações |
| ------- | ------ | --------------- | ----------- |
| **Refatoração e Snapping no MR #880** | Concluído | [MR #880 no KDE Invent](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/880) | Correção no arrasto e alinhamento de marcadores |

---

## 4. Entregas Individuais

| Integrante | Contribuições | Links (Diário de Bordo) | Observações |
| ---------- | ------------- | ----------------------- | ----------- |
| Caetano Santos Lucio | *[Inserir contribuições]* | [Diário de Bordo](../contribuicoes_individuais/CaetanoLucio-180144979/Sprint4.md) | Pendente |
| Davi Rodrigues Nunes | *[Inserir contribuições]* | [Diário de Bordo](../contribuicoes_individuais/DaviRodrigues-232014413/sprint4.md) | Pendente |
| Gustavo Oki de Freitas Rodrigues | *[Inserir contribuições]* | [Diário de Bordo](../contribuicoes_individuais/GustavoOki-231034716/sprint4.md) | Pendente |
| Julia dos Reis Teixeira Massuda | *[Inserir contribuições]* | [Diário de Bordo](../contribuicoes_individuais/JuliaMassuda-231035150/sprint4.md) | Pendente |
| João Pedro Rodrigues | *[Inserir contribuições]* | [Diário de Bordo](../contribuicoes_individuais/JoaoRodrigues-231035150/sprint4.md) | Pendente |
| Karolina Vieira Barbosa | *[Inserir contribuições]* | [Diário de Bordo](../contribuicoes_individuais/KarolinaVieira-202045820/sprint4.md) | Pendente |
| Letícia da Silva Monteiro | *[Inserir contribuições]* | [Diário de Bordo](../contribuicoes_individuais/LeticiaMonteiro-231026859/sprint4.md) | Pendente |
| **Lucas Mendonça Arruda** | Refatoração da captura do mouse no QML, criação de funções no C++ para mover o marcador na tela sem salvar direto no histórico e integração do cálculo de snapping na timeline.| [Diário de Bordo](../contribuicoes_individuais/LucasArruda-231035464/Sprint4.md) | **Concluído** |

---

## 5. Maiores Avanços

- **Implementação de Snapping:** Ajuste do comportamento do marcador para alinhar-se aos pontos de corte da timeline, convertendo a movimentação do mouse baseando-se no zoom e na taxa de FPS do projeto.

---

## 6. Maiores Dificuldades

- **Inconsistências em Ferramentas de CI:** Adaptação a validadores automatizados que geraram falhas por códigos legados do repositório local, exigindo modificações pontuais de contorno na configuração de build para testar a entrega.

---

## 7. Lições Aprendidas

- **Restrições de Componentes Visuais Padrão:** Identificação de que mecanismos genéricos de interface ocultam dados de coordenadas necessários para interações matemáticas precisas com grades de tempo estruturadas.
