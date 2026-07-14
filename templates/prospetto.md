# Modello — Prospetto (Excel)

Tabella di raffronto, scadenzario, quadro sinottico. Base: `templates/assets/modello-prospetto.xlsx`.

Una tabella è la forma in cui un dato inventato è più difficile da individuare: sta in una cella, ha
l'aria di un fatto, e nessuno lo rilegge. Per questo qui la regola sulle fonti diventa strutturale.

## Regola strutturale

**Ogni riga che contiene un dato tratto dall'archivio ha una colonna `Fonte` con l'etichetta `[F#]`.**
Una riga senza fonte è una riga non verificabile: o si cita, o non si scrive. Un prospetto privo
della colonna Fonte non va consegnato.

## Struttura del foglio

**Foglio 1 — Prospetto**
Le colonne di merito (variano col tema), più le due obbligatorie:

| … colonne di merito … | Fonte | Nota |
|---|---|---|
| dati | `[F3]` | eventuale precisazione |

Se una cella è ignota perché l'archivio non la copre, si scrive **"non coperto"** — mai una stima,
mai una cella vuota che possa essere letta come zero.

**Foglio 2 — Fonti**
L'elenco delle etichette: `[F#]`, documento, pagina. È il foglio che permette a chi rilegge di
risalire all'originale.

**Foglio 3 — Lacune** *(se presenti)*
Le righe o le colonne che l'archivio non ha permesso di compilare, e perché.

## Forma

- Nessuna formula che calcoli su celle "non coperto": il totale di una colonna incompleta è un numero
  falso. Se il totale non è calcolabile, si scrive che non lo è.
- Intestazioni chiare, una riga sola. Niente celle unite: rendono il foglio inutilizzabile a valle.
