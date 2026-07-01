# Relatório de Contribuição – Sprint 4

**Disciplina:** Gestão de Configuração e Evolução de Software  
**Equipe:** Equipe Kdenlive  
**Comunidade/Projeto de Software Livre:** Kdenlive  
**Período da Sprint:** 09/06/2026 – 30/06/2026  

---

## 1. Resumo da Sprint

A Sprint 4 concentrou-se na evolução técnica das contribuições para o ecossistema do Kdenlive, no aprimoramento da documentação de contribuição e no estabelecimento de diretrizes sólidas de desenvolvimento local. As frentes de trabalho foram divididas em duas principais linhas de atuação:

1. **Evolução da Timeline e Sistema de Snapping (BUG 406887):** Reestruturação técnica do arrasto de marcadores de clipes no backend (C++) e frontend (QML). A nova arquitetura substituiu a mecânica padrão de Drag por uma manipulação manual de eventos de mouse, permitindo integrar o alinhamento magnético (*snapping*) aos pontos de corte da Timeline, além de otimizar a pilha de Undo/Redo (MR #880).
2. **Reestruturação e Expansão das Diretrizes de Contribuição:** Reformulação completa do arquivo `contributing.md` para torná-lo claro e acessível a iniciantes, alinhando as seções com as boas práticas recomendadas pela comunidade KDE (MR #905). Além disso, iniciou-se o mapeamento e a melhoria das diretrizes em `coding.md` (MR #906) e a estruturação de ambientes locais estáveis via Arch Linux no WSL para contornar incompatibilidades de dependências (Qt6, KDE Frameworks, MLT).

---

## 2. Objetivos da Sprint

- [x] Reformular o mecanismo de arrasto dos marcadores de clipes para suportar alinhamento magnético (*snapping*) na timeline.
- [x] Ajustar o tratamento de eventos de mouse no QML para separar movimentações visuais temporárias do registro histórico de Undo/Redo no C++.
- [x] Resolver erros e bloqueios de compilação local/CI gerados por restrições estritas de analisadores estáticos (`all_qmllint`).
- [x] Expandir e padronizar o guia de contribuição (`contributing.md`) seguindo os padrões reais da KDE.
- [x] Validar o setup de compilação em ambientes WSL contornando limitações de versionamento de bibliotecas através de distribuições Arch Linux.
- [x] Preencher os diários de bordo individuais com os relatos técnicos.

---

## 3. Entregas Coletivas

| Entrega | Status | Link/Referência | Observações |
| ------- | ------ | --------------- | ----------- |
| **Refatoração e Snapping no MR #880** | Concluído | [MR #880 no KDE Invent](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/880) | Substituição de Drag nativo por mouse tracking e cálculo de frame delta com snapping. |
| **Atualização do Guia de Contribuição** | Concluído | [MR #905 no KDE Invent](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/905) | Reformulação completa do arquivo `contributing.md` com padrões oficiais. |
| **Expansão das Diretrizes de Desenvolvimento** | Em andamento | [MR #906 no KDE Invent](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/906) | Proposta de melhoria no arquivo `coding.md` detalhando Qt6, MLT e KConfigXT. |

---

## 4. Entregas Individuais

| Integrante | Contribuições | Links (Diário de Bordo) | Observações |
| ---------- | ------------- | ----------------------- | ----------- |
| Caetano Santos Lucio | – | [Diário de Bordo](../contribuicoes_individuais/CaetanoLucio-180144979/Sprint4.md) | Pendente |
| Davi Rodrigues Nunes | – | [Diário de Bordo](../contribuicoes_individuais/DaviRodrigues-232014413/sprint4.md) | Pendente |
| Gustavo Oki de Freitas Rodrigues | – | [Diário de Bordo](../contribuicoes_individuais/GustavoOki-231034716/sprint4.md) | Pendente |
| Julia dos Reis Teixeira Massuda | – | [Diário de Bordo](../contribuicoes_individuais/JuliaMassuda-231035150/sprint4.md) | Pendente |
| João Pedro Rodrigues | – | [Diário de Bordo](../contribuicoes_individuais/JoaoRodrigues-231035150/sprint4.md) | Pendente |
| Karolina Vieira Barbosa | – | [Diário de Bordo](../contribuicoes_individuais/KarolinaVieira-202045820/sprint4.md) | Pendente |
| Letícia da Silva Monteiro | Atualização do guia de contribuição (`contributing.md`) e configuração do ambiente local de compilação. | [Diário de Bordo](../contribuicoes_individuais/LeticiaMonteiro-231026859/sprint4.md) | Concluído |
| Lucas Mendonça Arruda | Refatoração estrutural da captura de eventos do mouse no QML e backend em C++ (`TimelineController`), implementação de transações sem Undo/Redo (`moveClipMarkerWithoutUndo`) protegidas com `QMutexLocker` e `qBound`, mapeamento de coordenadas com `mapToItem`, cálculo dinâmico de deltas em frames proporcionais ao nível de zoom e qualificação de escopos no `Clip.qml` para validação do `qmllint` em CI. | [Diário de Bordo](../contribuicoes_individuais/LucasArruda-231035464/Sprint4.md) | Concluído |

*(Nota: Diários de bordo listados como "Pendente" referem-se a integrantes que ainda não enviaram seus relatórios desta sprint).*

---

## 5. Maiores Avanços

**Destaques da Sprint:**

- **Controle Preciso de Snapping:** Implementação com sucesso da atração magnética de marcadores calculando posições em frames de vídeo com base na escala de zoom e FPS do projeto, superando as limitações do componente genérico de arrasto.
- **Transação Eficiente de Undo/Redo:** Arquitetura de movimento dividida em duas etapas (atualização visual sem registro em tempo real e consolidação definitiva no fechamento do evento), poupando recursos e mantendo o histórico limpo para comandos Ctrl+Z.
- **Qualificação de Escopo no QML:** Resolução de avisos estritos de analisadores estáticos (`all_qmllint`) relacionados a acessos de variáveis não qualificados, assegurando a aprovação nos pipelines oficiais da KDE.
- **Infraestrutura Local de Desenvolvimento:** Compilação com sucesso do Kdenlive usando CMake, Ninja e ferramentas avançadas em WSL com Arch Linux, resolvendo gargalos de versionamento de dependências.

---

## 6. Maiores Dificuldades

**Principais desafios enfrentados:**

- **Rigidez do Pipeline com Linter Estrito:** Lidar com falhas de integração contínua (CI) motivadas por regras estritas do `qmllint` em arquivos legados (não modificados diretamente pela equipe), exigindo alterações pontuais para destravar as execuções de build.
- **Cálculos Matemáticos de Tempo e Coordenadas:** Converter interações baseadas em pixels de tela para frames lógicos da timeline de vídeo, considerando variações de zoom e taxas de frames.
- **Compatibilidade de Pacotes em Distros Tradicionais:** Incompatibilidade crônica das dependências avançadas de build (Qt6, KDE Frameworks, MLT) em distribuições comuns como Ubuntu via WSL, necessitando migração para ambientes Arch Linux para viabilizar testes.

---

## 7. Lições Aprendidas

- **Limitações do Componente de Drag do QML:** Componentes de arrasto de alto nível restringem o controle preciso sobre as posições dos eventos, tornando controles de eventos manuais a opção padrão para alinhamentos geométricos avançados.
- **Configuração como Primeiro Gargalo:** A preparação do ambiente de compilação de software multimídia de grande escala exige atenção especial às versões de bibliotecas de terceiros, tornando ambientes de distribuição *rolling release* mais adequados para desenvolvimento ativo.
- **Documentação como Facilitador de Onboarding:** Diretrizes estruturadas reduzem drasticamente o tempo necessário para entender regras internas de projetos complexos, otimizando o fluxo de novas contribuições.
