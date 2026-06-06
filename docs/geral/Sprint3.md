# Relatório de Contribuição – Sprint 3

**Disciplina:** Gestão de Configuração e Evolução de Software  
**Equipe:** Equipe Kdenlive  
**Comunidade/Projeto de Software Livre:** Kdenlive  
**Período da Sprint:** 26/05/2026 – 08/06/2026  

---

## 1. Resumo da Sprint

A Sprint 3 teve como foco a resolução de uma issue de usabilidade no Kdenlive relacionada à exportação de vídeos no formato WebP animado. A dupla Gustavo Oki e Davi Rodrigues Nunes identificou, implementou e testou a correção do BUG 508117, que impedia usuários de configurar o número de loops diretamente pela interface do Kdenlive ao exportar arquivos WebP animados. O trabalho resultou na submissão do Merge Request !891 ao repositório oficial do KDE.

Em paralelo, a dupla publicou a resposta elaborada na Sprint 2 na thread do MR !866, dando continuidade ao processo de revisão daquela contribuição anterior.

---

## 2. Objetivos da Sprint

- [x] Identificar e analisar o BUG 508117 no Bugzilla do KDE.
- [x] Implementar o campo "Loop Count" na interface de edição de presets de renderização do Kdenlive.
- [x] Adicionar o preset "WebP Animation" na categoria "Images sequence" do repositório de presets.
- [x] Testar localmente a solução e validar o parâmetro de loop no arquivo WebP gerado.
- [x] Submeter o Merge Request !891 ao repositório oficial do Kdenlive.
- [x] Publicar a resposta ao mantenedor na thread do MR !866.

---

## 3. Entregas Coletivas

| Entrega | Status | Link/Referência | Observações |
| ------- | ------ | --------------- | ----------- |
| **Resolução do BUG 508117** | Concluído | [BUG 483954 no Bugzilla](https://bugs.kde.org/show_bug.cgi?id=508117) | Adição do campo Loop Count para WebP animado |
| **Submissão do Merge Request !891** | Concluído | [MR !891 no KDE Invent](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/891) | Implementação do Loop Count no editor de presets |
| **Resposta ao mantenedor do MR !866** | Concluído | [MR !866 no KDE Invent](https://invent.kde.org/multimedia/kdenlive/-/merge_requests/866) | Resposta publicada com plano de ajustes |

---

## 4. Entregas Individuais

| Integrante | Contribuições | Links (Diário de Bordo) | Observações |
| ---------- | ------------- | ----------------------- | ----------- |
| Caetano Santos Lucio             |  | [Diário de Bordo](../contribuicoes_individuais/CaetanoLucio-180144979/Sprint3.md)    | Pendente   |
| Davi Rodrigues Nunes | Análise da issue e do comportamento do parâmetro `loop` no muxer WebP via FFmpeg e MLT. Investigação do bug onde o parâmetro `loop=0` não era incluído nos params por estar dentro de um bloco `if (gopSpinner->value() > 0)`. Participação na implementação e nos testes de validação com `webpmux`. Co-autoria no commit submetido. | [Diário de Bordo](../contribuicoes_individuais/DaviRodrigues-232014413/sprint3.md) | Concluído |
| Gustavo Oki de Freitas Rodrigues | Implementação das modificações nos 3 arquivos do projeto (`editrenderpreset_ui.ui`, `renderpresetdialog.cpp`, `renderpresetrepository.cpp`). Investigação e resolução do bug do parâmetro `loop` não sendo gerado. Testes locais com `webpmux` para validação do `Loop Count: 0`. Submissão e documentação do MR !891. | [Diário de Bordo](../contribuicoes_individuais/GustavoOki-231034716/sprint3.md) | Concluído |
| Julia dos Reis Teixeira Massuda  | –                                                                                                                                                   | [Diário de Bordo](../contribuicoes_individuais/JuliaMassuda-231035150/sprint2.md)    | Pendente    |
| João Pedro Rodrigues             | –                                                                                                                                                   | [Diário de Bordo](../contribuicoes_individuais/JoaoRodrigues-231035150/sprint2.md)   | Pendente    |
| Karolina Vieira Barbosa          | –                                                                                                                                                   | [Diário de Bordo](../contribuicoes_individuais/KarolinaVieira-202045820/sprint2.md)  | Pendente    |
| Letícia da Silva Monteiro        | –                                                                                                                                                   | [Diário de Bordo](../contribuicoes_individuais/LeticiaMonteiro-231026859/sprint2.md) | Pendente    |
| Lucas Mendonça Arruda            | –         | [Diário de Bordo](../contribuicoes_individuais/LucasArruda-231035464/Sprint2.md)     | Pendente   |

---

## 5. Maiores Avanços

- **Resolução de problema real de usabilidade:** Usuários não precisam mais executar `webpmux -set loop 0` manualmente após cada exportação WebP.
- **Integração com o pipeline MLT/FFmpeg:** Compreensão de como o MLT repassa parâmetros ao muxer avformat e como o parâmetro `loop` é tratado pelo muxer WebP do FFmpeg.
- **Adição de preset à interface:** O preset "WebP Animation" agora aparece corretamente na categoria "Images sequence" da janela de renderização.
- **Validação ponta a ponta:** A solução foi confirmada com `webpmux -info`, que retornou `Loop Count: 0` no arquivo gerado.

---

## 6. Maiores Dificuldades

- **Identificação do nome correto do parâmetro:** Inicialmente tentou-se `muxer_opt_loop`, mas o MLT exige simplesmente `loop`, passado diretamente como AVOption ao muxer.
- **Bug do bloco GOP:** O parâmetro `loop=0` estava sendo gerado dentro de um bloco `if (gopSpinner->value() > 0)`, e como o valor padrão do GOP é 0, o parâmetro nunca era incluído nos params finais.
- **FFmpeg sem suporte a libwebp_anim:** O FFmpeg distribuído pelo KDE Craft não foi compilado com `--enable-libwebp`, exigindo substituição manual das DLLs para viabilizar o teste local.
- **Preset WebP não aparecia na interface:** O `parseMltPresets()` só carregava presets da pasta `stills/` como "Images sequence", ignorando o preset de animação WebP que fica na raiz do avformat.

---

## 7. Lições Aprendidas

- **Camada de abstração do MLT:** O MLT possui sua própria forma de repassar opções ao FFmpeg, diferente da sintaxe de linha de comando. Parâmetros de muxer são passados diretamente como propriedades do consumer avformat.
- **Importância do teste ponta a ponta:** A validação com `webpmux -info` foi essencial para confirmar que o parâmetro estava chegando corretamente ao arquivo final, e não apenas à camada de interface.
- **Debugging incremental:** A investigação foi feita camada a camada — interface → preset salvo → script MLT → arquivo gerado — o que permitiu isolar exatamente onde o parâmetro estava se perdendo.

---

## 8. Planejamento para a Próxima Sprint (Sprint 4)

- [ ] Acompanhar o feedback dos mantenedores no MR !891 e realizar ajustes solicitados.
- [ ] Implementar os ajustes do MR !866 conforme resposta ao mantenedor (nome dinâmico da pasta, tipo do clipe na mensagem, opção configurável no menu de contexto).
- [ ] Registrar o progresso nos diários de bordo individuais.
