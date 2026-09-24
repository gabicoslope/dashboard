# Modelo de dados

Banco do artifact `https://claude.ai/artifact/BqAJBGBLZStHLV4hpahN5H`, lido e escrito
pela página via `claude.use("db")` e, fora dela, pela ferramenta `ArtifactData`.

Regras de acesso: as padrão (`read: view`, `write: interact`). O artifact é privado —
só a conta dona e quem ela compartilhar conseguem abrir.

## `compromissos/<id>`

Id gerado pelo cliente (`.add()`) ou pelo Claude. Um documento por compromisso.

| campo | tipo | observação |
| --- | --- | --- |
| `titulo` | string | obrigatório |
| `data` | string | `YYYY-MM-DD`, data local, obrigatório |
| `hora` | string | `HH:MM` em 24h; vazio = dia todo |
| `categoria` | string | slug de um documento de `categorias`; vazio vira "Sem categoria" |
| `local` | string | clínica, endereço, link da call |
| `notas` | string | texto livre, quebras de linha preservadas na página |
| `status` | string | `"aberto"` ou `"feito"` |
| `concluidoEm` | string | ISO 8601 quando marcado feito, senão `""` |
| `gcalId` | string | id do evento no Google Agenda; `""` se não houver |
| `origem` | string | `"chat"`, `"dashboard"` ou `"gcal"` |
| `criadoEm` | string | ISO 8601 |

A página assina `compromissos` com `orderBy("data", "desc").limit(400)` — ou seja,
uma janela dos 400 mais recentes. A poda dos 60 dias na rotina diária existe para essa
janela nunca engolir os compromissos futuros.

## `categorias/<slug>`

| campo | tipo | observação |
| --- | --- | --- |
| `nome` | string | rótulo exibido |
| `cor` | string | hex `#RRGGBB`; a página deriva o tom de fundo da pílula por alfa |
| `ordem` | number | ordena os chips e a lista lateral |

Escolha cores de luminosidade média: a mesma cor é usada no tema claro e no escuro.

## `meta/brief`

Documento único, reescrito a cada manhã.

| campo | tipo | observação |
| --- | --- | --- |
| `data` | string | `YYYY-MM-DD` do dia resumido; a página mostra "atualizado hoje" quando bate com hoje |
| `texto` | string | 2 a 4 frases |
| `destaques` | string[] | até 4 linhas curtas, exibidas como lista com seta |
| `geradoEm` | string | ISO 8601 |

## Cuidados

- Uma escrita por vez em cada documento, e só quando algo mudou de fato.
- `update()` exige que o documento exista; `set()` substitui inteiro.
- Escritas são last-writer-wins, sem transação. Ao escrever algo que você acabou de
  ler pelo `ArtifactData`, passe `if_version`.
- Teto de 5.000 documentos por artifact.
