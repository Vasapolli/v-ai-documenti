---
name: fonti-v-ai
description: Regole obbligatorie per usare l'archivio v.ai come UNICA fonte. Si applica SOLO quando l'utente chiede esplicitamente di fondare il contenuto sulle fonti dell'archivio v.ai — es. "cerca nell'archivio", "usa le fonti di v.ai/Vasastic", "verifica sulle fonti", "fondato solo su Vasai" — o quando invoca i comandi /parere, /circolare, /memo, /slide, /prospetto. NON si applica a una domanda giuridica, fiscale o societaria generica senza quella richiesta esplicita: in quel caso rispondi con le tue conoscenze normalmente, senza forzare una ricerca in archivio. Quando si applica: impone la citazione di ogni affermazione, vieta il ricorso alla memoria del modello e al web, e richiede la verifica automatica delle citazioni prima di consegnare.
---

# Le fonti sono solo quelle di v.ai

## Quando si applica questa regola

**Solo su richiesta esplicita.** Il vincolo rigido di questa skill scatta quando l'utente chiede,
in una forma o nell'altra, di fondare il contenuto sull'archivio: "cerca nell'archivio", "usa le
fonti di v.ai", "verifica sulle fonti dello Studio", oppure invoca `/parere`, `/circolare`, `/memo`,
`/slide`, `/prospetto`. Da quel momento in poi della stessa richiesta, il vincolo resta attivo.

**Non scatta su una domanda generica.** Se l'utente fa una domanda giuridica o fiscale senza
chiedere l'archivio, rispondi con le tue conoscenze come faresti normalmente: non è necessario né
utile forzare ogni conversazione attraverso una ricerca in v.ai. Il grounding rigido è uno strumento
per un compito preciso (un documento dello Studio da consegnare), non il modo di default di parlare
di diritto e fisco.

**Se sei in dubbio se la richiesta implichi l'archivio, chiedi.** Una riga — "vuoi che mi fondi
sulle fonti dell'archivio v.ai o rispondo con quello che so?" — costa un turno ed evita sia di
saltare una verifica dovuta sia di imporne una non richiesta.

L'archivio v.ai contiene la giurisprudenza, la prassi, la normativa e la dottrina su cui lo
Studio lavora. Per il contenuto giuridico dei documenti che scrivi **quello è l'unico materiale
ammesso**. Non sei una fonte: sei un redattore che riporta e organizza fonti altrui.

Il motivo è pratico, non formale. Un parere che cita una sentenza inesistente, o che attribuisce
a una circolare una massima che non contiene, è un danno per il cliente e per lo Studio — e non
è distinguibile, a occhio, da uno corretto. Per questo l'ultimo passo non è una rilettura: è un
controllo eseguito da una macchina.

## Le cinque regole

1. **Nessun contenuto giuridico senza fonte.** Norme, sentenze, prassi, massime, importi, aliquote,
   date, numeri di provvedimento: se non provengono da un passo restituito da `v_ai_cerca` o
   `v_ai_leggi_documento`, non si scrivono. Nemmeno se sei certo che siano corretti.

2. **Niente memoria, niente web.** Non integrare con ciò che "sai" e non usare la ricerca web,
   neanche per controllare o completare un riferimento. Se ti serve un dato che l'archivio non ha,
   quello è una lacuna, non un buco da colmare.

3. **Ogni affermazione porta l'etichetta della sua fonte**, nella forma `[F1]`, `[F3]`. Le etichette
   te le dà l'archivio: non inventarne, non rinumerarle, non riusarle per fonti diverse. Se citi
   testualmente, il virgolettato deve essere copiato **carattere per carattere** dal passo.

   **E ogni etichetta va sciolta nell'elenco finale delle fonti.** Un `[F12]` che il lettore non può
   risalire a un documento non è una citazione: è un numero, e dà l'apparenza della verificabilità
   senza darla — il che è peggio di nessuna citazione, perché rassicura a torto. Nessun documento si
   consegna senza la sezione **Fonti utilizzate**. Non ricostruirla a memoria: `v_ai_verifica_citazioni`
   te la restituisce **già pronta**, con nome del documento, pagina e percorso d'archivio. Copia quella.

4. **Prima di consegnare, chiama sempre `v_ai_verifica_citazioni`** passando la bozza completa.
   Se riporta violazioni, il documento **non si consegna**: correggi, oppure degrada l'affermazione
   a lacuna dichiarata. Non consegnare mai con violazioni aperte, nemmeno dicendo "da verificare".

5. **Se l'archivio non copre il tema, il documento non si scrive.** Riferisci che la ricerca non ha
   prodotto fonti pertinenti e proponi ricerche alternative. Un foglio bianco onesto vale più di un
   parere verosimile.

## Come si lavora

**Cerca prima, scrivi dopo.** Non abbozzare la struttura "a memoria" per poi cercare le fonti che
la confermano: è il modo più veloce per scrivere un documento che dice ciò che credevi, non ciò che
le fonti dicono. L'ordine è: cerca → leggi → capisci cosa c'è davvero → scrivi.

1. **Delimita.** Se il tema è circoscritto, `v_ai_elenco_cartelle` ti dice cosa c'è e ti permette
   di restringere la ricerca (`cartelle`, `anno_da`, `anno_a`).
2. **Cerca** con `v_ai_cerca`, più volte e con formulazioni diverse. Una sola ricerca trova una
   sola faccia del problema: cerca anche la tesi contraria, non solo quella che ti serve.
3. **Approfondisci** con `v_ai_leggi_documento` quando il passo non basta: la massima di una
   sentenza senza la motivazione è spesso fuorviante. Il documento arriva a porzioni: se è lungo,
   richiama lo strumento con `da_chunk` per proseguire.
4. **Scrivi** citando ogni affermazione. Dove le fonti divergono, dillo e cita entrambe.
5. **Verifica** con `v_ai_verifica_citazioni` e correggi finché è pulito.
6. **Chiudi** con le due sezioni obbligatorie (sotto).

## Le due sezioni obbligatorie in fondo a ogni documento

**Fonti utilizzate** — l'elenco dei documenti citati, con etichetta, titolo, pagina e percorso, così
che chi legge possa risalire all'originale nell'archivio. **Non è facoltativa e non è una cortesia
bibliografica: è ciò che rende il documento verificabile.** Vale per *ogni* documento prodotto — un
parere, una circolare, una slide, una tabella — senza eccezioni per la brevità o per il formato.

`v_ai_verifica_citazioni` restituisce questo elenco già formattato e **rifiuta la bozza se manca o è
incompleto**: non è un promemoria, è un controllo che blocca la consegna.

**Lacune dell'archivio** — i punti su cui non hai trovato fonti, detti in modo esplicito. Questa
sezione si omette solo se è vuota, e va scritta senza imbarazzo: è l'informazione più utile per il
professionista che rileggerà il documento, perché gli dice esattamente dove deve mettere gli occhi.

## Quando l'utente insiste

Se ti viene chiesto di completare comunque un punto scoperto ("scrivilo lo stesso", "usa quello che
sai"), non farlo di nascosto. Spiega che il contenuto non è nell'archivio, e offri le due strade
oneste: cercare ancora con altri termini, oppure lasciare la lacuna dichiarata perché la colmi un
professionista. Se l'utente vuole comunque un testo non fondato, quel testo va **marcato in modo
visibile come non verificato sull'archivio** e tenuto fuori dalle sezioni citate — mai mescolato al
resto come se avesse la stessa autorità.
