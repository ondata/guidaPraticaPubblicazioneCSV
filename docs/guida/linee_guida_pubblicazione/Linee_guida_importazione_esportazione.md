---
hide:
 - toc
# - navigation
title: Esportare un CSV da Excel o LibreOffice
---

L'**esportazione diretta** in formato `CSV` da **Excel** o da **Libreoffice Calc** può causare **problemi** se le tabelle di dati contengono: celle unite, formule, macro, schede di espansione dati o altre caratteristiche derivate dall'applicazione delle funzionalità proprie di questi strumenti.

Per **esportare correttamente** i dati tabellari dagli strumenti di elaborazione dei fogli di calcolo, è necessario considerare le seguenti **linee guida**:

- il separatore di campo della guida è la virgola e il separatore decimale è il punto. Excel prende il separatore dalle impostazioni di Windows, non dal nome del formato: su un computer con impostazioni italiane il file può uscire con `;` e con la virgola nei decimali, e va [convertito](#convertire-in-csv-con-libreoffice-calc) prima di pubblicarlo;
- non usare **celle unite**;
- non lasciare **righe e/o colonne vuote** tra i dati;
- controllare i **formati delle celle**: una formula esce con il valore calcolato, ma le celle escono come sono visualizzate, quindi un formato a 2 decimali arrotonda il dato e una data può uscire come `31/01/2023`. Prima di esportare, usa il formato Generale per i numeri, `aaaa-mm-gg` per le date e Testo per i codici.

Una buona pratica per **verificare** che i **dati esportati** siano formattati correttamente in `CSV` è quella di **aprire il file in un editor di testo** come Blocco note: deve esserci una riga per record, le lettere accentate devono essere leggibili (`città`, non `cittÃ `) e gli zeri iniziali devono esserci ancora (`082053`, non `82053`).

## Aprire un CSV in Excel senza rovinarlo

All'apertura di un CSV, Excel toglie gli zeri iniziali anche se il campo è tra virgolette, trasforma in date valori come `2023-07` e toglie il `+` dai numeri di telefono. Se Windows usa la virgola come separatore decimale, legge il punto come separatore delle migliaia: `1234.56` diventa `123456`, senza alcun avviso. Con un doppio clic, inoltre, un file separato da virgole può finire tutto in una sola colonna.

Per questo il doppio clic è sconsigliato. La procedura che lascia i valori integri è questa. È stata provata su Excel con i menu in inglese: i nomi italiani vengono dalla documentazione di Microsoft in italiano, tra parentesi c'è quello inglese. L'opzione del passaggio 2 non compare nella documentazione italiana e resta in inglese.

1. Dati > Da testo/CSV (Data > From Text/CSV), e scegli il file.
2. In Rilevamento del tipo di dati (Data Type Detection) scegli Do not detect data types.
3. Clicca Trasforma dati (Transform Data), poi Usa prima riga come intestazioni (Use First Row as Headers).
4. In Passaggi applicati (Applied Steps) elimina l'ultimo passaggio, Tipo modificato (Changed Type).
5. Clicca Chiudi & Carica (Close & Load).

Tutte le colonne restano testo. Per farci calcoli, una colonna di numeri va convertita prima del passaggio 5, come spiega [la documentazione di Microsoft](https://support.microsoft.com/it-it/excel/set-a-locale-or-region-for-data-power-query): clic destro sull'intestazione della colonna, Cambia tipo > Uso delle impostazioni locali (Change Type > Using Locale); nella finestra Modifica tipo con impostazioni locali (Change Type with Locale) scegli il tipo [Numero decimale](https://support.microsoft.com/it-it/excel/add-or-change-data-types-power-query) e una lingua che usa il punto decimale, come l'inglese. Questa conversione non è stata provata per questa guida, e Microsoft scrive l'etichetta in modi diversi da una pagina all'altra.

## Salvare un CSV da Excel

- si raccomanda di **esportare** i dati tabellari in formato **`CSV`** utilizzando la **codifica standard dei caratteri `UTF-8`**;
- il formato «CSV UTF-8» di Excel conserva tutti i caratteri e aggiunge il BOM. Meglio pubblicare il file senza BOM, ma un file che lo contiene non è sbagliato: per toglierlo vedi [più sotto](#togliere-il-bom);
- il formato «CSV» semplice scrive in Windows-1252: `à` e `€` restano, mentre caratteri come `ł` o `日` diventano `?` e non si possono più recuperare;
- se la versione di Excel utilizzata non salva direttamente il file di dati codificato come `UTF-8`, è consigliabile **utilizzare una procedura di conversione di formato** che garantisca questa codifica di caratteri, ad esempio con LibreOffice Calc.

## Convertire in CSV con LibreOffice Calc

Se il file esce da Excel con `;` e la virgola nei decimali, LibreOffice Calc lo converte senza usare il terminale. I nomi italiani vengono dal pacchetto di traduzione di LibreOffice e dalla sua guida, tra parentesi c'è quello inglese.

1. File > Apri (File > Open), e scegli il file. Nella finestra Importazione testo (Text Import) imposta Tipo di carattere (Character set) su Unicode (UTF-8) e Impostazioni locali (Locale) su Italiano (Italia), e controlla che il separatore riconosciuto sia `;`. Nella guida di LibreOffice queste due voci si chiamano Set di caratteri e Lingua.
2. Nella griglia in basso clicca l'intestazione di ogni colonna con codici, telefoni o mesi, e imposta Tipo colonna (Column type) su Testo (Text). Per le date come `31/01/2023` scegli Data (GMA), cioè giorno, mese e anno (Date (DMY)). Lascia Standard le colonne con i numeri. Poi clicca OK.
3. Seleziona una colonna con i numeri e apri Formato > Celle (Format > Cells), scheda Numeri (Numbers). Imposta Lingua (Language), che nella versione di LibreOffice in sviluppo diventa Impostazioni locali, su Inglese (USA), e Codice del formato (Format code) su `General`. Ripeti per ogni colonna con i numeri. Per gli importi, che devono avere sempre lo stesso numero di decimali, usa il codice `0.00` al posto di `General`. Per le colonne con le date, nella stessa scheda, imposta Codice del formato su `AAAA-MM-GG`.
4. File > Salva con nome (File > Save As), formato Testo CSV (.csv), spunta Modifica impostazioni filtro (Edit filter settings) e clicca Salva. Se chiede quale formato tenere, scegli Usa il formato Testo CSV (Use Text CSV Format).
5. Nella finestra Esportazione file di testo (Export Text File) imposta Set di caratteri (Character set) su Unicode (UTF-8), perché il valore proposto può essere ISO-8859-1. Separatore di campo (Field delimiter) su `,`, Separatore di testo (String delimiter) su `"`, e lascia la spunta su Salva il contenuto della cella come mostrato (Save cell content as shown). Poi clicca OK.
6. Apri il file con un editor di testo e controlla il risultato.

Il risultato è un file con `,` e `.`: `1234,56` diventa `1234.56`, `31/01/2023` diventa `2023-01-31`, mentre zeri iniziali e `+` restano. L'importazione e il salvataggio sono stati provati sull'interfaccia di LibreOffice per Windows, in inglese, con il punto come separatore decimale. Il tipo Data (GMA) del passaggio 2, il passaggio 3 e la spunta del passaggio 5 sono stati provati solo con comandi, da riga di comando e con LibreOffice 25.2, impostato su Italiano (Italia): la voce di menu non è stata provata.

Che cosa succede se salti un passaggio, nella stessa prova:

- **Senza il formato inglese sulle colonne con i numeri**: se LibreOffice è impostato in italiano, i numeri escono come `"1234,56"`, con la virgola e tra virgolette, con o senza la spunta del passaggio 5. Il file non rispetta la regola del punto decimale.
- **Senza il formato `AAAA-MM-GG` sulle date**: la colonna esce nel formato della lingua di LibreOffice. In italiano resta `31/01/2023`; in inglese diventa `01/31/2023` e `01/12/2023` diventa `12/01/2023`, con giorno e mese scambiati. Se la colonna è lasciata Standard l'esito è lo stesso.
- **Con la colonna delle date in Testo**: `31/01/2023` esce così com'è, e va riscritta a parte.
- **Con il formato `General`**: gli zeri finali spariscono, `1250,00` diventa `1250`. Il valore non cambia. Con il formato `0.00` esce `1250.00`.
- **Togliendo la spunta del passaggio 5**: il formato `0.00` non viene più applicato e `1250,00` esce come `1250`. Numeri e date non escono tra virgolette.

## Togliere il BOM

Il BOM (Byte Order Mark) è un segno invisibile all'inizio del file, che indica la codifica. Alcuni programmi lo leggono come parte del nome della prima colonna, e CSV Lint lo segnala come errore «Whitespace»: non è un problema dei dati (vedi la [cassetta degli attrezzi](Cassetta_attrezzi.md)).

Se il file ha già `,` e `.`, per togliere il BOM basta aprirlo e salvarlo con LibreOffice Calc senza cambiare i valori. Segui i passaggi qui sopra con due differenze: al passaggio 2 imposta su Testo tutte le colonne, e salta il passaggio 3. Il separatore da controllare al passaggio 1 è `,`.

Provato da riga di comando con LibreOffice 25.2 su Linux: il file esce uguale a quello di partenza, senza BOM e con i fine riga cambiati da CRLF a LF. Anche la conversione da `;` a `,` qui sopra toglie il BOM.

## Per chi usa il terminale

La stessa conversione per togliere il BOM si fa con un comando. Qui ci sono cinque colonne, tutte di tipo Testo (`1/2/2/2/3/2/4/2/5/2` indica la colonna e il tipo: `1` Standard, `2` Testo, `4` Data GMA):

```bash
soffice --headless \
  --infilter='CSV:44,34,76,1,1/2/2/2/3/2/4/2/5/2,1040' \
  --convert-to 'csv:Text - txt - csv (StarCalc):44,34,76,1,,0,false,true,false,false,false' \
  --outdir uscita dati.csv
```

Con un file separato da `;` il primo `44` diventa `59` e le colonne con i numeri vanno lasciate al tipo `1`. Questo comando però non assegna formati di cella: se il profilo di LibreOffice è in italiano, i decimali restano con la virgola, e le date vanno come spiegato sopra.
