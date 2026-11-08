# Log

## 2026-11-08

- Conversione con LibreOffice provata sull'interfaccia in italiano (26.2, Windows): corretti tre nomi di voci e la rimozione del BOM, che dall'interfaccia richiede un foglio nuovo. 
- Excel provato con i menu in italiano: corretti i nomi, conversione dei numeri provata, «CSV UTF-8 (delimitato da virgole)» esce con `;` su Windows in italiano.
- Conversione con LibreOffice riscritta: procedura base con tutte le colonne in Testo, passaggi sui formati solo per decimali con la virgola e date non ISO. Spiegati BOM e motivo per toglierlo. Ritocchi residui delle riletture.
- Rilettura indipendente prima del rilascio: corretti codifica in ingresso, colonne con il punto decimale, frase della clausola. Rilascio v1.0.1.

## 2026-11-07

- Dopo la v1.0: rilettura indipendente delle ultime correzioni, frasi e rimandi corretti sul sito; l'archivio Zenodo resta quello del tag.
- Rilascio v1.0 su GitHub e Zenodo, DOI 10.5281/zenodo.24043615: esempio unico delle biblioteche, schede su modello unico, pagine generali riscritte; revisione tecnica e di linguaggio indipendenti. Corretto l'effetto della spunta «come mostrato» di LibreOffice, tolte le vecchie tabelle.
- Revisione della guida su quattro filoni (standard, PA e norme, comunicazione, strumenti): 96 segnalazioni, decise le regole di fondo.
- Scelte: separatore `,` e decimale `.`, valore mancante come cella vuota, meglio senza BOM, Table Schema prima di CSVW, lettore principale chi usa un foglio di calcolo, nome «Guida pratica alla pubblicazione di dati in CSV».
- Corretti errori negli esempi, link rotti, note di lavoro, strumenti superati, affermazioni su Excel, residui spagnoli e provenienza.
- Tolta la pagina dei buoni esempi, in attesa di esempi italiani validati (ANPR, Avellino, Prato).
- Rilascio v0.9 su GitHub e Zenodo, DOI 10.5281/zenodo.24042988.
- Nuove pagine: le 15 regole, dati personali, esempi di CSV italiani; nuove sezioni: schema e validazione, norme, codici italiani. Conversione con LibreOffice provata con agent-desktop.
- CI aggiornata: `mkdocs-material` 9.8.1, `mkdocs build --strict` prima del deploy.
