---
description: Redige un parere sull'archivio v.ai, con citazioni verificate
argument-hint: [quesito]
---

Redigi un **parere** sul quesito: $ARGUMENTS

Applica le skill `fonti-v-ai` e `redazione-documenti`, e la struttura di `templates/parere.md`.

Vincoli non negoziabili:
- Il contenuto viene **solo** da `v_ai_cerca` / `v_ai_leggi_documento`. Niente memoria, niente web.
- Cerca più volte e con formulazioni diverse, **inclusa la tesi contraria**, prima di scrivere.
- Ogni affermazione porta la sua etichetta `[F#]`.
- Prima di consegnare chiama `v_ai_verifica_citazioni` sulla bozza completa e correggi finché è pulita.
- Se il quesito è ambiguo (annualità, soggetto, imposta), chiedi chiarimenti **prima** di cercare.
- Se l'archivio non copre il tema, non scrivere il parere: dillo e proponi altre ricerche.
