# v.ai — Documenti

Plugin per Claude Cowork / Claude Code che redige documenti dello Studio **fondati esclusivamente
sulle fonti dell'archivio v.ai**: pareri, circolari, memo di ricerca, slide, prospetti Excel.

Ogni affermazione porta la citazione della fonte, e prima della consegna le citazioni vengono
**verificate a macchina** contro i passi realmente restituiti dall'archivio: una citazione inventata,
o un virgolettato attribuito a un documento che non lo contiene, blocca la consegna.

## Cosa contiene

- **Connector MCP `v_ai`** → gli strumenti `v_ai_cerca`, `v_ai_leggi_documento`,
  `v_ai_verifica_citazioni`, `v_ai_elenco_cartelle` (il server vive nell'app VasAI: `api/mcp.php`).
- **Skill `fonti-v-ai`** → le regole sul vincolo delle fonti. È il cuore del plugin.
- **Skill `redazione-documenti`** → il metodo e i formati di uscita.
- **Comandi** → `/parere`, `/circolare`, `/memo`, `/slide`, `/prospetto`.
- **Modelli** → `templates/` (struttura dei documenti) e `templates/assets/` (carta intestata e
  modelli grafici).

## Installazione

Serve solo l'indirizzo del server MCP (in produzione: `https://vasai.vasapolli.it/mcp`):

```bash
export V_AI_MCP_URL="https://ai.vasapolli.it/mcp"
```

Poi, da Claude Code o Cowork:

```
/plugin marketplace add /home/vasapolli/v-ai-documenti
/plugin install v-ai-documenti@vasapolli
/mcp                      ← al primo uso apre il browser: accedi col tuo account VasAI e concedi l'accesso
```

**Nessun token da chiedere all'amministratore**: l'autenticazione è OAuth. Ogni collega entra col
proprio account e vede **solo i documenti del suo gruppo** — gli stessi che vede dalla Chat web.

> Per script e prove da riga di comando resta possibile un token creato a mano:
> `php /var/www/elastic/scripts/mcp_token.php create <email> cli 90`, da passare in
> `Authorization: Bearer <token>`.

## Portarlo su un'altra installazione di VasAI

Il plugin non ha nulla di cablato. Per un altro studio o un altro server servono due gesti:

1. **`V_AI_MCP_URL`** → l'indirizzo del proprio server MCP.
2. **`templates/assets/`** → sostituire `carta-intestata.docx`, `modello-slide.pptx` e
   `modello-prospetto.xlsx` con quelli dello studio.

Nessuna modifica al codice del plugin né al server MCP.

## Aggiungere un tipo di documento

I tipi di documento sono **dati, non codice**:

1. Crea `templates/<nuovo-tipo>.md` con struttura, tono e sezioni obbligatorie (copia uno dei
   modelli esistenti come traccia).
2. Aggiungi la riga nella tabella dei tipi in `skills/redazione-documenti/SKILL.md`.
3. Se vuoi anche lo slash command, crea `commands/<nuovo-tipo>.md` sul modello di `commands/parere.md`.

Il server MCP non va toccato.

## Il limite da conoscere

Un plugin **non può disattivare** la ricerca web né la memoria del modello: le skill le vietano, ma
è un divieto scritto. Ciò che rende il vincolo reale è `v_ai_verifica_citazioni`, che confronta la
bozza con i passi effettivamente restituiti dall'archivio. Per questo la chiamata di verifica prima
della consegna non è una formalità: è l'unico punto in cui il vincolo diventa un fatto.
