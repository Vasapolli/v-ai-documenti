# NOTES — plugin v-ai-documenti

> ## ⚠️ PRIMA DI OGNI COMMIT: incrementa `version`
>
> In `.claude-plugin/plugin.json`. **Se non lo fai, il push non arriva ai client**: Claude vede lo
> stesso numero di versione e conclude che non c'è niente di nuovo. Nessun errore, nessun avviso —
> semplicemente il plugin resta quello vecchio e ci si perde un'ora a capire perché.
>
> Aggiornamento lato client: `/plugin marketplace update vasapolli` poi `/reload-plugins`.
> Meglio ancora: `/plugin` → Marketplaces → `vasapolli` → **Enable auto-update** (per i marketplace
> di terze parti è disattivato di default).

Note di lavoro (non documentazione: quella è in `README.md`). Piano completo:
`~/.claude/plans/vorrei-creare-una-skill-bright-lightning.md`.

## Stato al 14/07/2026

| Pezzo | Stato |
|---|---|
| Server MCP + 4 tool (`/var/www/elastic/api/mcp*.php`) | **Fatto e testato su dev.** |
| Patch retrieval (`cost_source`, `chunk_index`) | **Fatta, servizio riavviato**, costi visibili come `mcp_*`. |
| Plugin (skill, comandi, modelli) | **Scritto.** Non ancora provato dentro Cowork/Claude Code. |
| nginx `location = /mcp` | **Fatto** (14/07, ore 11). `https://ai.vasapolli.it/mcp` risponde: handshake, 4 strumenti, ricerca OK. |
| OAuth (Fase B) | Non iniziato. Oggi si usa un token bearer creato a mano. |
| Modelli grafici (`.docx`/`.pptx`/`.xlsx`) | **Mancano**: vedi `templates/assets/README.md`. |

Token attivo: `l.calabrese@vasapolli.it`, etichetta `cowork`, 90 giorni (ruolo admin → bypassa l'ACL,
quindi **non** è l'utente giusto per collaudare i permessi: per quello serve un utente non-admin).

## Prossimo passo

Installare il plugin e far scrivere un parere vero, poi giudicare la qualità dell'uscita:

```bash
export V_AI_MCP_URL="https://ai.vasapolli.it/mcp"
export V_AI_TOKEN="<token>"
# in Claude Code:  /plugin marketplace add /home/vasapolli/v-ai-documenti
#                  /plugin install v-ai-documenti@vasapolli
#                  /parere deducibilità dei costi black list …
```

## Decisioni prese, e perché

- **Il registro delle fonti sta sul server, non nel prompt.** Ogni chunk consegnato al modello è
  salvato in `mcp_citations` col suo testo esatto. È l'unico modo per cui `v_ai_verifica_citazioni`
  possa dire "questo virgolettato nella fonte non c'è": senza registro, la verifica sarebbe il
  modello che controlla sé stesso.
- **Il confronto delle citazioni ignora spazi, trattini e accenti** (`mcp_squeeze`). Il testo estratto
  dai PDF è tipograficamente rotto: parole incollate (`delimitarel'ambito`) e sillabazione di fine
  riga (`sia supe-riore`). Senza questa tolleranza, una citazione **fedele** veniva bocciata come
  inventata — falso allarme che avrebbe reso lo strumento inservibile. La severità resta dove serve:
  sul testo che nella fonte non esiste.
- **`top_k` viene troncato lato MCP.** Il retrieval in modo `chat` espande il contesto e restituisce
  molti più passi di quanti richiesti (98 per una richiesta da 3): riversarli tutti saturava il
  contesto del modello.
- **I tipi di documento sono dati** (`templates/*.md`), non codice: aggiungerne uno non tocca il
  server MCP. Requisito esplicito di redistribuibilità.

## Trappole note

- **Un plugin non può disattivare la ricerca web di Cowork.** Le skill la vietano, ma il divieto è
  scritto: ciò che lo rende reale è la verifica meccanica. Se un giorno si potesse disabilitare i
  tool nativi per sessione, sarebbe da fare.
- Le etichette `F#` vivono per token e durano 7 giorni (`mcp_citations`, TTL). Sessioni diverse dello
  stesso utente **condividono** il registro finché il token è lo stesso: le etichette non si
  rinumerano, e va bene così (una fonte già vista mantiene la sua sigla).
- Gli admin bypassano l'ACL: per collaudare i permessi serve sempre un utente non-admin.
