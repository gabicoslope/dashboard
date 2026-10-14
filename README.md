# Agenda do Dia

Dashboard pessoal de compromissos, separados por categoria, com um resumo reescrito
todo dia de manhã.

**Dashboard:** https://claude.ai/artifact/BqAJBGBLZStHLV4hpahN5H

## Como funciona

O dashboard é um Artifact publicado no claude.ai. A página é o arquivo
[`agenda.html`](agenda.html) deste repositório; os dados ficam no banco do próprio
artifact (capacidade `db`), que sobrevive a republicações e é privado à conta dona.

Três formas de colocar compromisso lá dentro:

1. **Pelo chat.** Você manda em linguagem normal — "dentista quinta 14h", "reunião
   de equipe amanhã 10h" — e o Claude classifica na categoria, grava no banco e cria
   o evento no Google Agenda (`gabicoslopee@gmail.com`), guardando o `gcalId` no
   documento para não duplicar depois.
2. **Pelo botão "Novo compromisso"** na própria página.
3. **Pela rotina das 8h**, que importa eventos novos do Google Agenda.

## A rotina da manhã

Routine `trig_015vKMWqK8izZzxpkQNhzG1Z`, cron `0 11 * * *` (08:00 em
America/Sao_Paulo), abrindo uma sessão nova a cada disparo. Ela:

- importa do Google Agenda os eventos de hoje até 7 dias à frente que ainda não
  estejam no banco;
- apaga compromissos com mais de 60 dias, para o banco não crescer sem limite
  (o teto é 5.000 documentos por artifact);
- reescreve `meta/brief` com o resumo do dia;
- responde o mesmo resumo no chat, que vira notificação no celular.

O texto integral do prompt da rotina está em
[`docs/rotina-diaria.md`](docs/rotina-diaria.md).

## Categorias

| slug | nome | cor |
| --- | --- | --- |
| `trabalho` | Trabalho | `#3B74D5` |
| `pessoal` | Pessoal | `#9A5FD0` |
| `saude` | Saúde | `#2E9E6B` |
| `medico` | Médico | `#E0605C` |
| `familia` | Família | `#E19A2F` |
| `financeiro` | Financeiro | `#2AA0A6` |
| `estudos` | Estudos | `#C25BA0` |
| `casa` | Casa | `#7C8A3E` |

Para acrescentar, renomear ou recolorir, edite os documentos da coleção
`categorias` — a página lê a lista do banco, não tem nada fixo no código.

## Publicar uma alteração da página

Edite `agenda.html` e republique **na mesma URL**, senão nasce um artifact novo e
vazio:

```
Artifact(action="publish", url="https://claude.ai/artifact/BqAJBGBLZStHLV4hpahN5H",
         file_path="agenda.html")
```

O modelo de dados está em [`docs/modelo-de-dados.md`](docs/modelo-de-dados.md).

## Ideias de vídeos

Mande no chat o link de um vídeo do YouTube, Instagram ou TikTok. O Claude tira só a
dica, direta, e salva como Google Doc numa pasta por tema dentro de
[Ideias de Vídeos](https://drive.google.com/drive/folders/1DmN5L0Ph8V7x8-Ny5614UxD2TFMOPAJT)
no Drive. Passo a passo, pastas e custos em
[`docs/ideias-de-videos.md`](docs/ideias-de-videos.md).
