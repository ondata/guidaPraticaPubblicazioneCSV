# Registro delle modifiche

## Dopo la 1.0.1

Correzioni sul sito, non comprese nell'archivio Zenodo della 1.0.1: vocabolari nazionali del Catalogo della semantica dei dati, con il comando per confrontare una colonna con un vocabolario; spiegato come compilare il numero di versione nella bozza di clausola.

## 1.0.1 - 2026-11-08

Correzioni rispetto all'archivio della 1.0.

- Conversione con LibreOffice riscritta: procedura base con tutte le colonne in Testo, passaggi sui formati solo per decimali con la virgola e date non ISO, codifica scelta in base al file.
- BOM: aprendo e salvando un file dall'interfaccia di LibreOffice il BOM resta, quindi i dati vanno copiati in un foglio nuovo. La pagina ora dice che cos'è e perché toglierlo.
- Procedure provate con i menu in italiano su LibreOffice 26.2 ed Excel: corretti i nomi delle voci, provata la conversione dei numeri in Excel, segnalato che «CSV UTF-8 (delimitato da virgole)» con Windows in italiano esce con `;`.
- Comando da terminale: con un file separato da `;` e punto decimale le colonne con i numeri restano di tipo Testo, altrimenti `1.234` diventa `1234`.
- Strumenti di controllo: solo DuckDB, Miller e Frictionless, tolti csvkit e daff. Nuovi controlli regola per regola, comandi di DuckDB e Miller provati su DuckDB 2.0.0 e Miller 6.22.0, anche su Windows.
- BOM e doppio clic in Excel, letture sicure per chi riusa i dati, forma NFC, dimensione e impronta del file, FAIR e Data on the Web Best Practices.
- Aggiunti tra gli strumenti senza terminale Open Data Editor, SIMBA di AgID e il validatore CSV della Commissione europea, anche attraverso la sua API.
- Altre correzioni: frasi rotte in P11 e P08, rimandi della sezione per il terminale, schema in pagina allineato al file, formulazione su AgID e separatore, clausola per i capitolati, ritocchi delle riletture.

Limiti noti: restano quelli della 1.0 sui dati personali, su datos.gob.es e sul tema del sito.

## 1.0 - 2026-11-07

- Esempio unico delle biblioteche in tutte le schede, con CSV, schema e dizionario in `docs/risorse/esempi/`, validati in automatico.
- Le 15 schede riscritte su un modello unico: regola, così sì e così no, perché, casi particolari, come si fa, vedi anche.
- Introduzione, formato CSV, dizionario dei dati, strumenti, codici, archiviazione e fonti riscritti.
- Pagina Excel e LibreOffice riordinata, con menu in italiano e con la dichiarazione di che cosa è stato provato.
- Menu riordinato: regole, pratica, approfondimenti.
- Tolte le vecchie tabelle in `docs/risorse/tabelle/`: restano nell'archivio della 0.9.

Limiti noti:

- la procedura di Excel è provata con i menu in inglese, e quella di LibreOffice in parte senza interfaccia: i nomi italiani dei menu non sono stati cliccati;
- la pagina sui dati personali non è stata rivista da un RPD (Responsabile della protezione dei dati) o da un giurista;
- la conferma di datos.gob.es sulle condizioni di riuso è stata chiesta e non è ancora arrivata;
- Material for MkDocs, il tema del sito, finisce il supporto il 5 maggio 2027.

## 0.9 - 2026-11-07

Prima versione numerata. Il testo è utilizzabile e gli errori noti sono corretti, ma la revisione non è finita.

- Regole allineate: separatore `,` e decimale `.`, cella vuota per i valori mancanti, intestazione sempre presente, serie storiche in forma lunga, unità di misura nel nome della colonna, codici come testo.
- Nuove pagine: le 15 regole in una pagina, dati personali, esempi di CSV italiani.
- Nuove sezioni: schema e validazione, la guida e le norme, codici italiani, conversione con LibreOffice.
- Esempi corretti, strumenti chiusi tolti, residui del testo spagnolo sostituiti, provenienza e licenza dichiarate.

Da fare per la 1.0:

- esempio unico delle biblioteche al posto delle auto;
- introduzione e schede riscritte in un italiano meno da traduzione;
- nomi dei menu di Excel e LibreOffice in italiano;
- Cassetta degli attrezzi riscritta.
