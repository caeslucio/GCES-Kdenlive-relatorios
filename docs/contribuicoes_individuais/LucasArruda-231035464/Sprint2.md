# Diário de Bordo – Lucas

**Disciplina:** GERÊNCIA DE CONFIGURAÇÃO E EVOLUÇÃO DE SOFTWARE  
**Equipe:** GCES 2026.1 – Kdenlive  
**Comunidade/Projeto de Software Livre:** [Kdenlive](https://invent.kde.org/multimedia/kdenlive)  
**Sprint:** Sprint 2 (12/05/2026 – 25/05/2026)  
**Matrícula:** 231035464   
**GitHub:** [@lucasarruda](https://github.com/lucasarruda9)  
**KDE Invent:** [@lucasma](https://invent.kde.org/lucasma)

---

## 1. Resumo da Sprint 2 (12/05/2026 - 25/05/2026)

A Sprint 2 foi focada exclusivamente na contribuição para o projeto de código aberto Kdenlive. O trabalho envolveu desde a triagem de tarefas voltadas para novos contribuidores nas plataformas do KDE até a implementação de código e submissão de um Merge Request para a base principal do software. A atividade prática consistiu em resolver uma demanda de usabilidade aberta desde 2019, aplicando lógica em QML para permitir o arrasto de marcadores de clipe na linha de tempo sem interferir nas interações de clique já existentes.

### 1.1 Identificação do Bug

O processo iniciou-se com o mapeamento de relatórios de falhas no ecossistema Bugs.kde.org, utilizando o filtro de buscas voltado a "junior-jobs" do Kdenlive. O objetivo foi selecionar uma demanda de usabilidade reportada diretamente pela comunidade que trouxesse um desafio sob medida para novos contribuidores. Dessa forma, foi selecionado o BUG 406887, uma pendência aberta desde 2019.

![Lista de Bugs da KDE"]()
*Figura 1: Lista de Bugs do KDE com os filtros "junior-jobs" e "kdenlive"*

### 1.2 Descrição do Bug

O BUG 406887 apontava uma limitação na usabilidade do timeline do Kdenlive, sendo impossível mover marcadores de clipe diretamente arrastando-os com o mouse. No comportamento original, para alterar a posição de um marcador, o usuário era obrigado a abrir um menu de edição e digitar o novo valor de tempo manualmente. A proposta consistia em permitir a movimentação do marcador na timeline pelo mouse.

![Issue 2172"]()
*Figura 2: BUG 406887*

## 2. Histórico de Versões

| Versão | Descrição                                                      | Autor(es)                            | Data       | 
|--------|----------------------------------------------------------------|--------------------------------------|------------|
| 1.0    |  Adicionando template e resumo introdutório da Sprint2                |  [Lucas Mendonça](https://github.com/lucasarruda9)  | 24/05/2026 | 
| 1.1    |  Adicionando Identificação e descrição da nova funcionalidade (BUG 406887)               |  [Lucas Mendonça](https://github.com/lucasarruda9)  | 24/05/2026 | 

