# Rotina diária das 8h

Routine `trig_015vKMWqK8izZzxpkQNhzG1Z` — cron `0 11 * * *` em UTC, que é 08:00 em
America/Sao_Paulo. Cada disparo abre uma sessão nova, então o prompt é autossuficiente.
Notificação push ligada.

## Estado dos conectores

A Routine foi criada **sem conectores guardados**: esta organização não permite
passá-los por essa via. Na prática as sessões disparadas rodam sem as ferramentas
`mcp__*`, então o passo 3 (importar do Google Agenda) é pulado e o resumo sai só com o
que já está no banco.

Para ligar: abra a Routine em https://claude.ai/settings/routines, adicione o conector
Google Calendar e salve. O prompt já cobre os dois casos.

## Prompt

```
Rotina diária do dashboard "Agenda do Dia".

Artifact: https://claude.ai/artifact/BqAJBGBLZStHLV4hpahN5H
Fuso horário: America/Sao_Paulo. Google Agenda principal: gabicoslopee@gmail.com
Responda sempre em português do Brasil, direto e sem enrolação.

Faça nesta ordem:

1. Descubra a data de hoje com `TZ=America/Sao_Paulo date +%F` (e o dia da semana).

2. Carregue a ferramenta ArtifactData (ToolSearch com "select:ArtifactData") e leia o banco do artifact:
   - action "list", collection "compromissos"
   - action "list", collection "categorias"

3. Leia o Google Agenda de hoje até 7 dias à frente (mcp__Google_Calendar__list_events, calendarId "gabicoslopee@gmail.com", orderBy "startTime"; carregue com ToolSearch se preciso). Para cada evento que ainda NÃO exista em "compromissos" (compare pelo campo gcalId), crie o documento correspondente com:
   { titulo, data: "YYYY-MM-DD", hora: "HH:MM" (vazio se for dia todo), categoria: <slug de "categorias" mais provável>, local, notas: "", status: "aberto", gcalId: <id do evento>, origem: "gcal", criadoEm: <ISO agora>, concluidoEm: "" }
   Nunca duplique. Nunca invente compromisso que não esteja no banco nem no Google Agenda. Se o Google Agenda não estiver disponível nesta sessão, siga com o que está no banco e diga isso no fim.

4. Nada é marcado como "feito" automaticamente — só a usuária faz isso.

5. Limpeza: exclua de "compromissos" os documentos com data anterior a 60 dias atrás.

6. Escreva o resumo em meta/brief (ArtifactData action "set", collection "meta", doc_id "brief"):
   {
     "data": "<YYYY-MM-DD de hoje>",
     "texto": "<2 a 4 frases: quantos compromissos hoje, qual é o primeiro e a que horas, o que exige preparo ou deslocamento, e o que está atrasado. Tom direto e caloroso, sem emoji, sem bajulação.>",
     "destaques": ["<até 4 linhas curtas: itens de hoje com hora e categoria, pendências atrasadas, e o que vem amanhã>"],
     "geradoEm": "<ISO de agora>"
   }
   Se o dia estiver vazio, diga isso com naturalidade e cite o próximo compromisso da semana.

7. Termine respondendo no chat o mesmo resumo em texto corrido, seguido da lista de hoje (hora — título — categoria) e depois dos atrasados, se houver. Esse texto vira a notificação no celular, então deixe ele útil sozinho.
```

## Mexer na rotina

Mudar horário, nome ou ligar/desligar: `update_trigger` com o `trigger_id`, ou a tela de
Routines no claude.ai. Trocar o horário significa recalcular para UTC — 08:00 em
Brasília é `0 11 * * *`; 07:00 seria `0 10 * * *`.
