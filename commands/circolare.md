---
description: Redige una circolare o newsletter sull'archivio v.ai, con citazioni verificate
argument-hint: [novità da segnalare]
---

Redigi una **circolare** su: $ARGUMENTS

Applica le skill `fonti-v-ai` e `redazione-documenti`, e la struttura di `templates/circolare.md`.

Vincoli non negoziabili:
- Il contenuto viene **solo** dall'archivio v.ai. Niente memoria, niente web.
- Ogni affermazione porta la sua etichetta `[F#]`.
- Non inventare l'impatto pratico: se le fonti non dicono cosa cambia in concreto, riferisci il
  contenuto del provvedimento e dichiara che l'impatto non è desumibile dall'archivio.
- Prima di consegnare chiama `v_ai_verifica_citazioni` e correggi finché è pulita.
