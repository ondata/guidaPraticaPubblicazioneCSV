---
title: Esportare un CSV da Excel o LibreOffice
---

# Esportare un CSV da Excel o LibreOffice

Prima di esportare, sistema il foglio:

- **Celle unite:** non usarle.
- **Righe e colonne vuote:** non lasciarne tra i dati.
- **Formule:** nel CSV esce il valore calcolato.
- **Formati delle celle:** le celle escono come sono visualizzate, quindi un formato a 2 decimali arrotonda il dato e una data può uscire come `31/01/2023`. Usa il formato Generale per i numeri, un formato a 2 decimali per gli importi, `aaaa-mm-gg` per le date e Testo per i codici.

Questa guida usa la virgola come separatore e il punto per i decimali. Excel prende il separatore dalle impostazioni di Windows: con impostazioni italiane il file può uscire con `;` e con la virgola nei decimali, e va [convertito](#convertire-in-csv-con-libreoffice-calc) prima di pubblicarlo.

Dopo l'esportazione apri il file con un editor di testo, come Blocco note. Controlla che ci sia una riga per ogni record, che le lettere accentate siano leggibili (`città`, non `cittÃ `) e che gli zeri iniziali ci siano ancora (`082053`, non `82053`).

## Salvare un CSV da Excel

Usa File > Salva con nome e scegli il formato «CSV UTF-8».

- **«CSV UTF-8»:** conserva tutti i caratteri e aggiunge il BOM (Byte Order Mark, un segno invisibile all'inizio del file). Meglio pubblicare il file senza BOM, ma un file che lo contiene non è sbagliato: per toglierlo vedi [più sotto](#togliere-il-bom).
- **«CSV» semplice:** scrive in Windows-1252. `à` e `€` restano, mentre caratteri come `ł` o `日` diventano `?` e non si possono più recuperare. Meglio evitarlo.
- **Se la tua versione di Excel non ha «CSV UTF-8»:** converti il file con [LibreOffice Calc](#convertire-in-csv-con-libreoffice-calc).

## Convertire in CSV con LibreOffice Calc

Se il file esce da Excel con `;` e la virgola nei decimali, LibreOffice Calc lo converte senza usare il terminale. I nomi italiani vengono dal pacchetto di traduzione di LibreOffice e dalla sua guida, tra parentesi c'è quello inglese.

1. File > Apri (File > Open), e scegli il file. Nella finestra Importazione testo (Text Import) imposta Tipo di carattere (Character set) su Unicode (UTF-8) e Impostazioni locali (Locale) su Italiano (Italia), e controlla che il separatore riconosciuto sia `;`.
2. Nella griglia in basso clicca l'intestazione di ogni colonna con codici, telefoni o mesi, e imposta Tipo colonna (Column type) su Testo (Text). Per le date come `31/01/2023` scegli Data (GMA), cioè giorno, mese e anno (Date (DMY)). Lascia Standard le colonne con i numeri. Poi clicca OK.
3. Imposta i formati in Formato > Celle (Format > Cells), scheda Numeri (Numbers), una colonna alla volta:
    - **Numeri:** Lingua (Language) su Inglese (USA), Codice del formato (Format code) su `General`.
    - **Importi:** come i numeri, ma con il codice `0.00`, perché devono avere sempre lo stesso numero di decimali.
    - **Date:** Codice del formato su `AAAA-MM-GG`.
4. File > Salva con nome (File > Save As), formato Testo CSV (.csv), spunta Modifica impostazioni filtro (Edit filter settings) e clicca Salva. Se chiede quale formato tenere, scegli Usa il formato Testo CSV (Use Text CSV Format).
5. Nella finestra Esportazione file di testo (Export Text File) imposta Set di caratteri (Character set) su Unicode (UTF-8), perché il valore proposto può essere ISO-8859-1. Separatore di campo (Field delimiter) su `,`, Separatore di testo (String delimiter) su `"`, e lascia la spunta su Salva il contenuto della cella come mostrato (Save cell content as shown). Poi clicca OK.
6. Apri il file con un editor di testo e controlla il risultato.

Il risultato è un file con `,` e `.`: `1234,56` diventa `1234.56`, `31/01/2023` diventa `2023-01-31`, mentre zeri iniziali e `+` restano.

!!! note "Come è stata provata"

    L'importazione e il salvataggio sono stati provati sull'interfaccia di LibreOffice per Windows, con i menu in inglese e con il punto come separatore decimale. Formati delle colonne ed esportazione sono stati provati senza interfaccia, con LibreOffice 25.2 impostato su Italiano (Italia): le voci di menu italiane di quei passaggi vengono dal pacchetto di traduzione e non sono state cliccate. Nella guida di LibreOffice, Tipo di carattere e Impostazioni locali si chiamano Set di caratteri e Lingua; nella versione in sviluppo Lingua diventa Impostazioni locali.

Che cosa succede se salti un passaggio:

- **Senza il formato inglese sulle colonne con i numeri**: se LibreOffice è impostato in italiano, i numeri escono come `"1234,56"`, con la virgola e tra virgolette, con o senza la spunta del passaggio 5. Il file non rispetta la regola del punto decimale.
- **Senza il formato `AAAA-MM-GG` sulle date**: la colonna esce nel formato della lingua di LibreOffice. In italiano resta `31/01/2023`; in inglese diventa `01/31/2023` e `01/12/2023` diventa `12/01/2023`, con giorno e mese scambiati. Se la colonna è lasciata Standard l'esito è lo stesso.
- **Con la colonna delle date in Testo**: `31/01/2023` esce così com'è, e va riscritta a parte.
- **Con il formato `General`**: gli zeri finali spariscono, `1250,00` diventa `1250`. Il valore non cambia. Con il formato `0.00` esce `1250.00`.
- **Togliendo la spunta del passaggio 5**: il formato `0.00` non viene più applicato e `1250,00` esce come `1250`. Numeri e date non escono tra virgolette.

## Togliere il BOM

Alcuni programmi lo leggono come parte del nome della prima colonna, e CSV Lint lo segnala come errore «Whitespace»: non è un problema dei dati (vedi gli [strumenti di controllo](Cassetta_attrezzi.md)).

Se il file ha già `,` e `.`, per togliere il BOM basta aprirlo e salvarlo con LibreOffice Calc senza cambiare i valori. Segui i passaggi qui sopra con due differenze: al passaggio 2 imposta su Testo tutte le colonne, e salta il passaggio 3. Il separatore da controllare al passaggio 1 è `,`.

Anche la conversione da `;` a `,` qui sopra toglie il BOM.

## Aprire un CSV in Excel senza rovinarlo

All'apertura di un CSV, Excel toglie gli zeri iniziali anche se il valore è tra virgolette, può trasformare in date valori come `2023-07` e toglie il `+` dai numeri di telefono. Se Windows usa la virgola come separatore decimale, legge il punto come separatore delle migliaia: `1234.56` diventa `123456`, senza alcun avviso. Con un doppio clic, inoltre, un file separato da virgole può finire tutto in una sola colonna.

Per questo il doppio clic è sconsigliato. Questa procedura lascia i valori integri. Tra parentesi c'è il nome inglese del menu.

1. Dati > Da testo/CSV (Data > From Text/CSV), e scegli il file.
2. In Rilevamento del tipo di dati (Data Type Detection) scegli Do not detect data types.
3. Clicca Trasforma dati (Transform Data), poi Usa prima riga come intestazioni (Use First Row as Headers).
4. In Passaggi applicati (Applied Steps) elimina l'ultimo passaggio, Tipo modificato (Changed Type).
5. Clicca Chiudi & Carica (Close & Load).

Tutte le colonne restano testo. Per farci calcoli, una colonna di numeri va convertita prima del passaggio 5, come spiega [la documentazione di Microsoft](https://support.microsoft.com/it-it/excel/set-a-locale-or-region-for-data-power-query): clic destro sull'intestazione della colonna, Cambia tipo > Uso delle impostazioni locali (Change Type > Using Locale); nella finestra Modifica tipo con impostazioni locali (Change Type with Locale) scegli il tipo [Numero decimale](https://support.microsoft.com/it-it/excel/add-or-change-data-types-power-query) e una lingua che usa il punto decimale, come l'inglese. Questa conversione non è stata provata per questa guida.

!!! note "Come è stata provata"

    La procedura è stata provata su Excel con i menu in inglese, non su un Excel in italiano. I nomi italiani vengono dalla documentazione di Microsoft in italiano; l'opzione del passaggio 2 lì non compare e resta in inglese.

## Per chi usa il terminale

La stessa conversione per togliere il BOM si fa con un comando. Qui ci sono cinque colonne, tutte di tipo Testo (`1/2/2/2/3/2/4/2/5/2` indica la colonna e il tipo: `1` Standard, `2` Testo, `4` Data GMA):

```bash
soffice --headless \
  --infilter='CSV:44,34,76,1,1/2/2/2/3/2/4/2/5/2,1040' \
  --convert-to 'csv:Text - txt - csv (StarCalc):44,34,76,1,,0,false,true,true,false,false' \
  --outdir uscita dati.csv
```

Con un file separato da `;` il primo `44` diventa `59` e le colonne con i numeri vanno lasciate al tipo `1`. Questo comando però non assegna formati di cella: se il profilo di LibreOffice è in italiano, i decimali restano con la virgola, e le date vanno come spiegato sopra.

Provato con LibreOffice 25.2 su Linux: il file esce uguale a quello di partenza, senza BOM e con i fine riga cambiati da CRLF (ritorno a capo più nuova riga, tipico di Windows) a LF (solo nuova riga).

Nel comando, l'ultimo `true` dopo `,0,false,true,` corrisponde alla spunta del passaggio 5.
