# Diário de Bordo – Letícia da Silva Monteiro

**Disciplina:** Gestão da Configuração e Evolução de Software (GCES)  
**Equipe:** GCES 2026.1 – Kdenlive  
**Comunidade/Projeto de Software Livre:** [Kdenlive](https://invent.kde.org/multimedia/kdenlive)  
**Matrícula:** 231026859  
**GitHub:** [@LeticiaMonteiroo](https://github.com/LeticiaMonteiroo)  
**KDE Invent:** [@leticia](https://invent.kde.org/leticia)




# Diário de Bordo – Sprint 1

**Disciplina:** Gestão da Configuração e Evolução de Software (GCES)  
**Projeto:** Contribuição para o repositório open source [KDE Kdenlive](https://invent.kde.org/multimedia/kdenlive)  
**Área de contribuição:** Documentação de build e onboarding de desenvolvimento  
**Responsável:** Letícia Monteiro  

---

## Sobre a Contribuição

A contribuição realizada nesta Sprint teve como foco a melhoria da documentação de build do Kdenlive, localizada em `dev-docs/build.md`.

O objetivo principal foi tornar o processo de compilação e configuração do ambiente de desenvolvimento mais acessível para novos contribuidores, reduzindo ambiguidades e organizando melhor informações importantes sobre dependências, Craft, ferramentas opcionais e troubleshooting.

As alterações buscaram melhorar principalmente:

- Clareza da documentação;
- Experiência de onboarding;
- Separação entre etapas obrigatórias e opcionais;
- Organização do fluxo de build;
- Legibilidade para novos contribuidores.

---

## Entradas do Diário

---

### Entrada 01 — Exploração da Documentação Existente

Inicialmente foi realizado um estudo completo da documentação de build do Kdenlive para entender:

- Como o fluxo de compilação estava estruturado;
- Quais dependências eram realmente obrigatórias;
- Quais ferramentas eram opcionais;
- Quais partes poderiam gerar confusão para novos desenvolvedores.

Durante essa análise foi identificado que algumas seções misturavam:

- Explicações mais acessíveis para novos contribuidores;
- Melhor legibilidade das seções relacionadas ao Craft.
- instruções essenciais;
- ferramentas avançadas;
- otimizações de compilação.

**Merge Request:** [!869](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/869)  

## Lições Aprendidas

- Documentação técnica bem estruturada reduz significativamente a dificuldade de onboarding em projetos open source;
- Separar claramente funcionalidades obrigatórias e opcionais melhora a experiência de novos contribuidores;
- O uso de `rebase` é extremamente importante para manter a branch atualizada com as mudanças mais recentes do projeto, evitando conflitos e inconsistências;
- No GitLab, parte desse processo pode ser feito automaticamente durante Merge Requests, mas ainda é essencial acompanhar constantemente se a branch está sincronizada com a branch principal.

---

## Plano Pessoal para a Próxima Sprint (Sprint 2)

- [ ] Continuar aprimorando a documentação técnica do projeto;
- [ ] Participar de novas contribuições no código-fonte do Kdenlive;
- [ ] Aprender mais sobre o fluxo de revisão e integração contínua no GitLab;
- [ ] Acompanhar feedbacks da comunidade e ajustar contribuições conforme necessário.