---
description: Costruisce un prospetto Excel (raffronto, scadenzario) fondato sull'archivio v.ai
argument-hint: [oggetto del prospetto]
---

Costruisci un **prospetto** su: $ARGUMENTS

Applica le skill `fonti-v-ai` e `redazione-documenti`, e la struttura di `templates/prospetto.md`.

Vincoli non negoziabili:
- **Ogni riga con un dato d'archivio ha la colonna `Fonte` con l'etichetta `[F#]`.** Una tabella
  senza colonna delle fonti non è verificabile e non va consegnata.
- Cella ignota → si scrive "non coperto". Mai una stima, mai una cella vuota.
- Nessun totale calcolato su colonne incomplete: se non è calcolabile, si dichiara.
- Fogli obbligatori: Prospetto, Fonti, e Lacune se ce ne sono.
- Prima di consegnare chiama `v_ai_verifica_citazioni` sul contenuto testuale del prospetto.
