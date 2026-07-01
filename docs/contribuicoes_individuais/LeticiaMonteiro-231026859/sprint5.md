# Diário de Bordo – Letícia da Silva Monteiro

**Disciplina:** Gestão de Configuração e Evolução de Software  
**Equipe:** GCES 2026.1 – Kdenlive  
**Comunidade/Projeto:** [KDE / Kdenlive](https://invent.kde.org/multimedia/kdenlive)  
**Matrícula:** 231026859  
**GitHub:** [@LeticiaMonteiroo](https://github.com/LeticiaMonteiroo)  
**KDE Invent:** [@leticia](https://invent.kde.org/leticia)
---

## 1. Resumo da Sprint

Durante esta sprint, o principal objetivo foi preparar o ambiente de desenvolvimento para contribuir com o projeto Kdenlive e compreender sua estrutura de desenvolvimento.

Inicialmente, foram realizadas diversas tentativas de configuração do ambiente utilizando o WSL com Ubuntu. Entretanto, devido à incompatibilidade entre as versões das dependências exigidas pelo projeto (principalmente Qt6, KDE Frameworks e MLT) e os pacotes disponíveis na distribuição utilizada, tornou-se inviável prosseguir por esse caminho.

Após analisar a documentação oficial do projeto e compreender melhor os requisitos de compilação, foi adotada uma nova estratégia utilizando o Arch Linux no WSL, permitindo instalar versões mais recentes das bibliotecas necessárias. Com isso, foi possível compilar o Kdenlive com sucesso e executar a aplicação localmente.

Além da configuração do ambiente, foi realizada uma análise da documentação destinada aos desenvolvedores. Durante essa análise foi identificado que o arquivo `coding.md`, apesar de conter informações importantes, apresentava descrições bastante resumidas sobre alguns conceitos fundamentais do projeto.

Como proposta de melhoria, foi elaborada uma nova versão desse documento, mantendo seu propósito original, porém ampliando as explicações sobre as principais tecnologias utilizadas pelo Kdenlive, regras importantes de desenvolvimento e boas práticas para novos contribuidores.

[Merge Request](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/906)

---

## 2. Atividades Realizadas

| Data | Atividade | Tipo | Link/Referência | Status |
|------|-----------|------|-----------------|--------|
| — | Estudo da documentação oficial do Kdenlive | Estudo | README e documentação oficial | Concluído |
| — | Configuração inicial do ambiente utilizando WSL (Ubuntu) | Configuração | Ambiente local | Concluído |
| — | Pesquisa e resolução de problemas relacionados às dependências do projeto | Pesquisa | Documentação oficial | Concluído |
| — | Migração do ambiente para Arch Linux no WSL | Configuração | Ambiente local | Concluído |
| — | Compilação completa do Kdenlive utilizando CMake e Ninja | Código | Ambiente local | Concluído |
| — | Execução da aplicação compilada | Teste | Ambiente local | Concluído |
| — | Estudo da documentação para desenvolvedores | Documentação | `coding.md` | Concluído |
| — | Elaboração de proposta de melhoria para o arquivo `coding.md` | Documentação | Pull Request (em elaboração) | Em andamento |

---

## 3. Maiores Avanços

- Configuração completa do ambiente de desenvolvimento para o Kdenlive.
- Compreensão do processo de compilação utilizando CMake e Ninja.
- Entendimento da organização geral do repositório.
- Familiarização com as principais tecnologias utilizadas pelo projeto, como Qt6, KDE Frameworks e MLT.
- Identificação de uma oportunidade de melhoria na documentação técnica destinada aos desenvolvedores.

---

## 4. Maiores Dificuldades

- Configurar corretamente o ambiente de desenvolvimento devido às diversas dependências exigidas pelo projeto.
- Resolver incompatibilidades entre versões das bibliotecas disponíveis no Ubuntu e aquelas requeridas pelo Kdenlive.
- Compreender a relação entre o WSL, as distribuições Linux e o ambiente de compilação.
- Entender o fluxo de build do projeto utilizando CMake e Ninja.

---

## 5. Aprendizados

Durante esta sprint foram adquiridos diversos conhecimentos relacionados ao desenvolvimento de projetos de software livre, entre eles:

- Processo de compilação utilizando CMake e Ninja.
- Estrutura geral do projeto Kdenlive.
- Funcionamento do MLT como motor de processamento multimídia.
- Papel do Qt6 e dos KDE Frameworks dentro da aplicação.
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
- [ ] Identificar uma issue de baixa complexidade para realizar a primeira contribuição em código.