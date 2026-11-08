---
title: Esportare un CSV da Excel o LibreOffice
---

# Esportare un CSV da Excel o LibreOffice

Per lavorare con i CSV, LibreOffice Calc è più comodo di Excel: in Excel il separatore dipende dalle impostazioni di Windows, e aprire un CSV senza alterare i valori richiede più passaggi.

Prima di esportare, sistema il foglio:

- **Celle unite:** non usarle.
- **Righe e colonne vuote:** non lasciarne tra i dati.
- **Formule:** nel CSV esce il valore calcolato.
- **Formati delle celle:** le celle escono come sono visualizzate, quindi un formato con meno decimali del dato lo arrotonda e una data può uscire come `31/01/2023`. Usa il formato Generale per i numeri, un formato a 2 decimali per gli importi, `aaaa-mm-gg` per le date e Testo per i codici.

Questa guida usa la virgola come separatore e il punto per i decimali. Excel prende il separatore dalle impostazioni di Windows: con impostazioni italiane il file può uscire con `;` e con la virgola nei decimali, e va [convertito](#se-i-decimali-hanno-la-virgola-o-le-date-non-sono-aaaa-mm-gg) prima di pubblicarlo.

Dopo l'esportazione apri il file con un editor di testo, come Blocco note. Controlla che ci sia una riga per ogni record, che le lettere accentate siano leggibili (`città`, non `cittÃ `) e che gli zeri iniziali ci siano ancora (`082053`, non `82053`).

## Salvare un CSV da Excel

Usa File > Salva con nome e, in Salva come, scegli «CSV UTF-8 (delimitato da virgole)».

- **«CSV UTF-8 (delimitato da virgole)»:** conserva tutti i caratteri e aggiunge il BOM (Byte Order Mark, un segno invisibile all'inizio del file). Nonostante il nome, con Windows in italiano il separatore è `;`, e il file va [convertito](#convertire-in-csv-con-libreoffice-calc). Meglio pubblicare il file senza BOM, ma un file che lo contiene non è sbagliato: per toglierlo vedi [più sotto](#togliere-il-bom).
- **«CSV (delimitato dal separatore di elenco)»:** scrive in Windows-1252. `à` e `€` restano, mentre caratteri come `ł` o `日` diventano `?` e non si possono più recuperare. Meglio evitarlo.
- **Se la tua versione di Excel non ha «CSV UTF-8»:** converti il file con [LibreOffice Calc](#convertire-in-csv-con-libreoffice-calc).

## Convertire in CSV con LibreOffice Calc

LibreOffice Calc cambia il separatore da `;` a `,` e porta il file in UTF-8 senza usare il terminale. I nomi dei menu sono quelli di LibreOffice in italiano, tra parentesi c'è quello inglese.

1. File > Apri (File > Open), e scegli il file. Nella finestra Importazione testo (Text Import) imposta Tipo di carattere (Character set) sulla codifica del file: Unicode (UTF-8) per un «CSV UTF-8», Europa occidentale (Windows-1252/WinLatin 1) per il CSV semplice di Excel. Nell'anteprima le lettere accentate devono essere leggibili. Controlla anche che il separatore riconosciuto sia quello del file, per esempio `;`.
2. Nella griglia in basso clicca l'angolo in alto a sinistra, così selezioni tutte le colonne, e imposta Tipo colonna (Column type) su Testo (Text). Poi clicca OK.
3. File > Salva con nome (File > Save As), in Salva come scegli Testo CSV (*.csv), spunta Modifica impostazioni filtro (Edit filter settings) e clicca Salva. Se chiede quale formato tenere, scegli Usa il formato Testo CSV (Use Text CSV Format).
4. Nella finestra Esportazione file di testo (Export Text File) imposta Set di caratteri (Character set) su Unicode (UTF-8), perché il valore proposto può essere un altro, come Europa occidentale (Windows-1252/WinLatin 1). Separatore di campo (Field delimiter) su `,`, Delimitatore di stringa (String delimiter) su `"`, e lascia la spunta su Salva il contenuto della cella come mostrato (Save cell content as shown). Poi clicca OK.
5. Apri il file con un editor di testo e controlla il risultato.

Il `;` diventa `,` e nessun valore cambia: zeri iniziali, `+`, numeri e date restano come sono. Basta questo se i numeri hanno già il punto decimale e le date sono già scritte come `2023-01-31`. Se il file di partenza aveva il BOM, lo ha anche quello salvato: per toglierlo vedi [più sotto](#togliere-il-bom).

### Se i decimali hanno la virgola o le date non sono AAAA-MM-GG

Con tutte le colonne in Testo questi valori non cambiano: `1234,56` esce come `"1234,56"` e `31/01/2023` resta così. Per convertirli, cambiano i passaggi 1 e 2 e se ne aggiunge uno prima di salvare:

1. Al passaggio 1 imposta anche Impostazioni locali (Locale) su Italiano (Italia).
2. Al passaggio 2, invece di selezionare tutte le colonne, clicca l'intestazione di ogni colonna e imposta Tipo colonna (Column type): Testo (Text) per codici, telefoni e mesi, Data (GMA), cioè giorno, mese e anno (Date (DMY)), per le date come `31/01/2023`, Standard per le colonne con i numeri che hanno la virgola, Testo per quelle che hanno già il punto. Poi clicca OK.
3. Prima di salvare, imposta i formati in Formato > Celle (Format > Cells), scheda Numeri (Numbers), una colonna alla volta:
    - **Numeri:** Impostazioni locali (Locale) su Inglese (USA). Il Codice del formato (Format Code) diventa da solo `General`.
    - **Importi:** come i numeri, ma con il codice `0.00`, perché devono avere sempre lo stesso numero di decimali.
    - **Date:** Codice del formato su `AAAA-MM-GG`.

Poi salva come ai passaggi 3 e 4 della procedura qui sopra. Il risultato è un file con `,` e `.`: `1234,56` diventa `1234.56`, `31/01/2023` diventa `2023-01-31`, mentre zeri iniziali e `+` restano.

Che cosa succede se salti un passaggio:

- **Senza il formato inglese sulle colonne con i numeri**: se LibreOffice è impostato in italiano, i numeri escono come `"1234,56"`, con la virgola e tra virgolette, con o senza la spunta del passaggio 4. Il file non rispetta la regola del punto decimale.
- **Senza il formato `AAAA-MM-GG` sulle date**: la colonna esce nel formato della lingua di LibreOffice. In italiano resta `31/01/2023`; in inglese diventa `01/31/23` e `01/12/2023` diventa `12/01/23`, con giorno e mese scambiati e l'anno a due cifre. Se la colonna è lasciata Standard, giorno e mese si scambiano allo stesso modo, ma l'anno resta a quattro cifre (`01/31/2023`).
- **Con la colonna delle date in Testo**: `31/01/2023` esce così com'è, e va riscritta a parte.
- **Con il formato `General`**: gli zeri finali spariscono, `1250,00` diventa `1250`. Il valore non cambia. Con il formato `0.00` esce `1250.00`.
- **Togliendo la spunta del passaggio 4**: il formato `0.00` non viene più applicato e `1250,00` esce come `1250`. Con i formati impostati, numeri e date non escono tra virgolette.

!!! note "Come è stata provata"

    Entrambe le procedure sono state provate sull'interfaccia di LibreOffice 26.2 per Windows, con i menu in italiano e impostato su Italiano (Italia). Quella con tutte le colonne in Testo su un file uscito da Excel con `;` e punto decimale e su uno con `,` e `.`, quella con i formati su un file con `;`, virgola nei decimali e BOM. I nomi inglesi vengono dall'interfaccia in inglese. Nella guida in linea di LibreOffice alcune voci hanno ancora il nome delle versioni precedenti: Set di caratteri per Tipo di carattere, Lingua per Impostazioni locali.

## Togliere il BOM

Il BOM (Byte Order Mark) è una sequenza di tre byte invisibili all'inizio del file, che segnala che il testo è in UTF-8. La aggiunge per esempio Excel quando salvi in «CSV UTF-8 (delimitato da virgole)». Un file che la contiene non è sbagliato, ma meglio pubblicarlo senza.

Il motivo per toglierlo è che alcuni programmi leggono quei byte come parte del nome della prima colonna. A vista il nome sembra giusto, ma uno script che cerca la colonna `codice_comune` non la trova, perché per lui si chiama `\ufeffcodice_comune`. CSV Lint lo segnala come errore «Whitespace»: non è un problema dei dati (vedi gli [strumenti di controllo](Cassetta_attrezzi.md)).

Per toglierlo con LibreOffice Calc non basta aprire il file e salvarlo: il file salvato ha ancora il BOM. I dati vanno copiati in un foglio nuovo:

1. Apri il file come ai passaggi 1 e 2 della [conversione](#convertire-in-csv-con-libreoffice-calc), con tutte le colonne in Testo.
2. Modifica > Seleziona tutto (Edit > Select All), poi Modifica > Copia (Edit > Copy).
3. File > Nuovo > Foglio elettronico (File > New > Spreadsheet), poi Modifica > Incolla (Edit > Paste).
4. Salva il foglio nuovo come ai passaggi 3 e 4 della conversione. Per un foglio nuovo, Salva come propone il formato di LibreOffice (.ods): va cambiato in Testo CSV (*.csv).

Provato con LibreOffice 26.2 per Windows: il file esce uguale a quello di partenza, senza BOM. Vale anche per un file appena convertito da `;` a `,`, che il BOM lo conserva.

## Aprire un CSV in Excel senza rovinarlo

All'apertura di un CSV, Excel toglie gli zeri iniziali anche se il valore è tra virgolette, può trasformare in date valori come `2023-07` e toglie il `+` dai numeri di telefono. Con Windows in italiano può leggere il punto come separatore delle migliaia: `1234.56` diventa `123456`, senza alcun avviso. Con un doppio clic, inoltre, un file separato da virgole può finire tutto in una sola colonna.

Per questo il doppio clic è sconsigliato. Questa procedura lascia i valori integri. Tra parentesi c'è il nome inglese del menu.

1. Dati > Da testo/CSV (Data > From Text/CSV), e scegli il file.
2. In Rilevamento del tipo di dati (Data Type Detection) scegli Non rilevare i tipi di dati (Do not detect data types).
3. Clicca Trasforma dati (Transform Data), poi Usa la prima riga come intestazione (Use First Row as Headers).
4. In Passaggi applicati (Applied Steps) elimina l'ultimo passaggio, Modificato tipo (Changed Type), con la X accanto al nome.
5. Clicca Chiudi e carica (Close & Load).

Tutte le colonne restano testo. Per farci calcoli, una colonna di numeri va convertita prima del passaggio 5, come spiega [la documentazione di Microsoft](https://support.microsoft.com/it-it/excel/set-a-locale-or-region-for-data-power-query): clic destro sull'intestazione della colonna, Modifica tipo > Uso delle impostazioni locali (Change Type > Using Locale); nella finestra Modifica tipo con impostazioni locali (Change Type with Locale) scegli il tipo [Numero decimale](https://support.microsoft.com/it-it/excel/add-or-change-data-types-power-query) e, in Impostazioni locali, una lingua che usa il punto decimale, come Inglese (Stati Uniti).

!!! note "Come è stata provata"

    La procedura e la conversione dei numeri sono state provate su Excel con i menu in italiano, su un Windows in italiano che usa il punto come separatore decimale. Con il rilevamento dei tipi lasciato attivo, `1234.56` è stato letto come `123456` anche in questa configurazione. I nomi inglesi vengono da una prova con i menu in inglese e dalla documentazione di Microsoft.

## Per chi usa il terminale

Il BOM si toglie anche con un comando, senza copiare i dati in un foglio nuovo: la conversione senza interfaccia non lo rimette. Qui ci sono cinque colonne, tutte di tipo Testo (`1/2/2/2/3/2/4/2/5/2` indica la colonna e il tipo: `1` Standard, `2` Testo, `4` Data GMA):

```bash
soffice --headless \
  --infilter='CSV:44,34,76,1,1/2/2/2/3/2/4/2/5/2,1040' \
  --convert-to 'csv:Text - txt - csv (StarCalc):44,34,76,1,,0,false,true,true,false,false' \
  --outdir uscita dati.csv
```

Con un file separato da `;` il primo `44` diventa `59`. Se i decimali hanno la virgola, le colonne con i numeri vanno al tipo `1`; se hanno già il punto, restano al tipo `2`, perché con il tipo `1` e il filtro italiano `1.234` diventerebbe `1234`. Questo comando però non assegna formati di cella: se il profilo di LibreOffice è in italiano, i decimali restano con la virgola, e le date vanno trattate come spiega la sezione [Convertire in CSV con LibreOffice Calc](#convertire-in-csv-con-libreoffice-calc).

Provato con LibreOffice 25.2 su Linux: il file esce uguale a quello di partenza, senza BOM e con i fine riga cambiati da CRLF (ritorno a capo più nuova riga, tipico di Windows) a LF (solo nuova riga). Con LibreOffice 26.2 su Windows il BOM sparisce allo stesso modo, e i fine riga restano CRLF.

Nel comando, l'ultimo `true` dopo `,0,false,true,` corrisponde alla spunta del passaggio 4 di quella conversione, Salva il contenuto della cella come mostrato.
