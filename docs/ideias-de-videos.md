# Ideias de Vídeos

A Gabi manda no chat um link de vídeo com uma boa ideia. O Claude tira só a dica do
vídeo, direta, e salva como Google Doc na pasta do tema certo, dentro de
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
| Produtos para Comprar | `1UB9mT8pSwluzoy7dypK3fwBG-7k5_WEx` |
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

- Para vídeo curto, passe um `prompt` pedindo a fala e o texto na tela, para
  extrair a dica.
- TikTok encurtado (`vm.tiktok.com`, `tiktok.com/t/`) não funciona: peça o link
  completo `tiktok.com/@usuario/video/<id>`.
- Sem créditos suficientes, avise e pare. Não troque por outra fonte.

## Relatório

Crie o doc com Drive `create_file`, `contentMimeType: "text/html"`, o HTML em
`textContent` e `parentId` = ID da pasta do tema. Título:
`AAAA-MM-DD · <título curto do vídeo>` (data de hoje em America/Sao_Paulo).

O doc é curto e direto: só a dica, sem resumo do vídeo, sem enrolação, sem
transcrição. Cabe numa tela. Em português:

1. **Link** do vídeo, numa linha só.
2. **A dica** — uma ou duas frases dizendo o que fazer.
3. **Como fazer** — só se a dica tiver passos: no máximo 5 itens curtos, cada um
   começando com um verbo.

Vídeo de produto vai para `Produtos para Comprar`, e o doc traz: nome do produto,
para que serve, onde comprar e preço (só se o vídeo disser).

Corte apresentação, história do autor, pedido de like, exemplos repetidos e
qualquer coisa que não seja a dica em si. Se o vídeo tiver mais de uma dica útil,
liste cada uma em uma linha.

Depois responda no chat só com o link do doc, a pasta e a dica em uma frase.
Vários links na mesma mensagem: um doc por vídeo.
