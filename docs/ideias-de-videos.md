# Ideias de Vídeos

A Gabi manda no chat um link de vídeo com uma boa ideia. O Claude pega o que foi dito,
escreve um relatório e salva como Google Doc na pasta do tema certo, dentro de
**Ideias de Vídeos** no Google Drive (`gabicoslopee@gmail.com`).

**Pasta raiz:** https://drive.google.com/drive/folders/1DmN5L0Ph8V7x8-Ny5614UxD2TFMOPAJT

## Pastas

| Tema | ID da pasta |
| --- | --- |
| Negócios e Dinheiro | `1g2JNpg8uLbMrcfvD2BaNOl7ExdI0tYVJ` |
| Conteúdo e Redes Sociais | `167LS3jyQUz5VAyU3Ui1gLfUl6nlmaXuj` |
| Produtividade e Organização | `1cCJsdIOvVlXIY5ooSL8XHIDnRNfdcXpv` |
| Saúde e Bem-estar | `1Ns-SqkbLfZAlhjxiw89471jp1mqZDfFG` |
| Casa e Decoração | `101Ftu54zjfh6qO_1GUO-zh9Mxt6EBNtr` |
| Tecnologia e IA | `1XXIcRAkHftDZ6nXMMdZPbaM25YWH_9OS` |
| Outros | `1Fkc0X1HUGQddj7RTdt2b8uFnrlU-F3zV` |

Se a Gabi disser o tema junto com o link ("isso é pra Casa"), use esse. Se nenhum
servir, use `Outros` ou, se ela pedir, crie uma subpasta nova na raiz com Drive
`create_file` (`contentMimeType: application/vnd.google-apps.folder`) e acrescente a
linha nesta tabela.

## Como pegar o conteúdo

A rede do container bloqueia YouTube e Instagram, então `yt-dlp` não funciona. Tudo
passa pelo conector **vidIQ**. Antes de começar, confira o saldo com
`vidiq_balance` (grátis); o plano dá 150 créditos por mês.

| Link | Ferramenta | Custo |
| --- | --- | --- |
| YouTube longo (`youtube.com/watch`, `youtu.be`) | `vidiq_video_transcript` | 5 |
| YouTube sem legenda | `vidiq_video_watch` — só depois de avisar a Gabi | 25 |
| Instagram Reels, TikTok, YouTube Shorts | `vidiq_watch_shortform_content` + `vidiq_job_poll` | 10 |

- Para vídeo curto, passe um `prompt` pedindo: transcrição de tudo que é falado,
  texto que aparece na tela e as ideias principais.
- TikTok encurtado (`vm.tiktok.com`, `tiktok.com/t/`) não funciona: peça o link
  completo `tiktok.com/@usuario/video/<id>`.
- Sem créditos suficientes, avise e pare. Não troque por outra fonte.

## Relatório

Crie o doc com Drive `create_file`, `contentMimeType: "text/html"`, o HTML em
`textContent` e `parentId` = ID da pasta do tema. Título:
`AAAA-MM-DD · <título curto do vídeo>` (data de hoje em America/Sao_Paulo).

Estrutura, em português:

1. **Cabeçalho** — link do vídeo, autor/canal, plataforma, duração.
2. **Em uma frase** — a ideia central.
3. **Ideias principais** — lista, cada item com uma ou duas linhas.
4. **Como aplicar** — passos práticos que a Gabi pode fazer, ligados à vida dela
   (negócio, conteúdo, casa, rotina) quando fizer sentido.
5. **Trechos marcantes** — frases citadas, com minutagem quando houver.
6. **Transcrição** — completa no YouTube; nos vídeos curtos, a fala transcrita e a
   descrição cena a cena.

Depois responda no chat só com o link do doc, a pasta onde ficou e a frase central.
Vários links na mesma mensagem: um doc por vídeo.
