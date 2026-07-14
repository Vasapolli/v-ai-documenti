---
name: redazione-documenti
description: Come si redigono i documenti dello Studio Vasapolli a partire dall'archivio v.ai — parere, circolare, memo di ricerca, slide, prospetto Excel. Contiene l'indice dei modelli, il flusso di lavoro comune e le regole di forma (tono, struttura, citazioni, formati di uscita .docx/.pdf/.pptx/.xlsx). Da usare ogni volta che l'utente chiede di scrivere uno di questi documenti.
---

# Redazione dei documenti dello Studio

Vale sempre e prima di tutto la skill **fonti-v-ai**: il contenuto viene solo dall'archivio, ogni
affermazione è citata, e la consegna passa da `v_ai_verifica_citazioni`. Qui c'è il *come* si
confeziona il documento, non il *da dove* viene il contenuto.

## I tipi di documento

| Tipo | Modello | Quando |
|---|---|---|
| Parere / memoria | `templates/parere.md` | Risposta ragionata a un quesito, con conclusioni argomentate. |
| Circolare / newsletter | `templates/circolare.md` | Segnalazione divulgativa di una novità a clienti o colleghi. |
| Memo di ricerca | `templates/memo-ricerca.md` | Rassegna di ciò che l'archivio contiene su un tema, senza tesi. |
| Slide | `templates/slide.md` | Materiale per convegni o formazione interna. |
| Prospetto | `templates/prospetto.md` | Tabella di raffronto, scadenzario, quadro sinottico. |

**Leggi il modello prima di scrivere.** Ogni modello fissa struttura, tono e sezioni obbligatorie:
non improvvisare un'impaginazione tua.

## Flusso

1. **Chiarisci il mandato.** Se il quesito è ambiguo (quale annualità? quale soggetto? quale
   imposta?), chiedi prima di cercare: una ricerca su un quesito sbagliato produce un documento
   perfettamente citato e perfettamente inutile.
2. **Ricerca** nell'archivio (vedi `fonti-v-ai`). Cerca anche la posizione contraria.
3. **Scegli il modello** e seguine la struttura.
4. **Scrivi** citando `[F#]` ogni affermazione.
5. **Verifica** con `v_ai_verifica_citazioni`. Correggi. Ripeti finché è pulito.
6. **Produci il file** nel formato richiesto (sotto).

## Forma

- **Lingua:** italiano, registro professionale. Frasi piane; niente enfasi retorica.
- **Onestà del dubbio:** se la giurisprudenza è divisa, si scrive che è divisa e si citano entrambi
  gli orientamenti. Non si sceglie il più comodo tacendo l'altro.
- **Niente riempitivi:** nessuna premessa generica sul contesto normativo se non serve al quesito.
- **Citazioni:** l'etichetta `[F#]` sta a fine periodo, prima del punto. Nel documento finale
  consegnato al cliente le etichette restano: sono il modo in cui chi rilegge risale alla fonte.

## Formati di uscita

Chiedi in che formato lo vuole, se non l'ha detto. I modelli grafici stanno in `templates/assets/`:

- **Word (`.docx`)** — usa `templates/assets/carta-intestata.docx` come base: mantieni stili,
  intestazione e piè di pagina, sostituisci il corpo.
- **PDF** — genera prima il `.docx`, poi converti, così l'impaginazione resta quella dello Studio.
- **PowerPoint (`.pptx`)** — parti da `templates/assets/modello-slide.pptx`.
- **Excel (`.xlsx`)** — parti da `templates/assets/modello-prospetto.xlsx`. Nei prospetti, ogni riga
  che contiene un dato tratto da una fonte porta l'etichetta `[F#]` in una colonna dedicata: una
  tabella senza colonna delle fonti non è verificabile e non va consegnata.

Se un file modello non è ancora disponibile, **dillo** e consegna in Markdown, senza inventare una
grafica dello Studio.

## Aggiungere un nuovo tipo di documento

Non serve toccare codice: si aggiunge un file in `templates/` con la struttura del nuovo documento
e una riga nella tabella qui sopra. Vedi `README.md`.
