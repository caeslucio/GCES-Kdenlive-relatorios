# Diário de Bordo – Letícia da Silva Monteiro

**Disciplina:** Gestão de Configuração e Evolução de Software  
**Equipe:** GCES 2026.1 – Kdenlive  
**Comunidade/Projeto:** [KDE / Kdenlive](https://invent.kde.org/multimedia/kdenlive)  
**Matrícula:** 231026859  
**GitHub:** [@LeticiaMonteiroo](https://github.com/LeticiaMonteiroo)  
**KDE Invent:** [@leticia](https://invent.kde.org/leticia)
---

## 1. Resumo da Sprint

Durante a análise da documentação feita essa semana foi identificado que o arquivo `coding.md`, apesar de conter informações importantes, apresentava descrições bastante resumidas sobre alguns conceitos fundamentais do projeto.

Como proposta de melhoria, foi elaborada uma nova versão desse documento, mantendo seu propósito original, porém ampliando as explicações sobre as principais tecnologias utilizadas pelo Kdenlive, regras importantes de desenvolvimento e boas práticas para novos contribuidores.

[Merge Request](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/906)

---

## 2. Atividades Realizadas

| Data | Atividade | Tipo | Link/Referência | Status |
|------|-----------|------|-----------------|--------|
| 28/06 | Estudo da documentação para desenvolvedores | Documentação | `coding.md` | Concluído |
| 28/06 | Elaboração de proposta de melhoria para o arquivo `coding.md` | Documentação | Pull Request (em elaboração) | Em andamento |

---

## 3. Maiores Avanços

- Identificação de uma oportunidade de melhoria na documentação técnica destinada aos desenvolvedores.

---

## 4. Maiores Dificuldades

- Conhecer todas as regras para contribuir com a comunidade que já a maior parte está fora do Gitlab 

---

## 5. Aprendizados

Durante esta sprint foram adquiridos diversos conhecimentos relacionados ao desenvolvimento de projetos de software livre, entre eles:

- Estrutura geral do projeto Kdenlive.
- Importância da documentação técnica para facilitar a entrada de novos colaboradores.
- Fluxo básico de contribuição para projetos open source.

Também foi possível perceber que uma boa documentação reduz significativamente a curva de aprendizado de novos desenvolvedores e evita dúvidas recorrentes durante o processo de contribuição.

---

## 6. Justificativa da Alteração Proposta

Durante a leitura do arquivo `coding.md`, foi observado que o documento apresenta informações importantes para o desenvolvimento do projeto, porém de forma bastante resumida.

Embora os conceitos estejam corretos, diversos tópicos fundamentais são apresentados sem contexto suficiente para auxiliar um novo desenvolvedor a compreender como essas tecnologias são utilizadas dentro do Kdenlive.

A proposta de alteração consiste em expandir esse documento sem modificar seu propósito original.

Entre as melhorias propostas estão:

- introdução explicando o objetivo do documento;
- organização dos conteúdos em seções mais claras;
- explicações mais detalhadas sobre Qt, KDE Frameworks, MLT e XMLGUI;
- documentação mais completa sobre o tratamento de Locale e utilização do `QLocale`;
- explicação do sistema de configurações (`KConfigXT`);
- inclusão de observações sobre arquivos gerados automaticamente;
- adição de referências úteis para consulta da documentação oficial.

Essas alterações tornam o documento mais acessível para novos colaboradores, preservando sua função como referência técnica rápida e reduzindo o tempo necessário para compreender as principais convenções adotadas pelo projeto.

Além disso, uma documentação mais completa contribui para padronizar futuras implementações, diminuir erros relacionados às regras internas do projeto e facilitar o processo de onboarding de novos membros da comunidade.

---

## 7. Plano Pessoal para a Próxima Sprint

- [ ] Finalizar a revisão do novo `coding.md`.
- [ ] Submeter um Pull Request com a melhoria da documentação.
- [ ] Participar das discussões da comunidade relacionadas à documentação.
- [ ] Estudar com maior profundidade a arquitetura interna do Kdenlive.
