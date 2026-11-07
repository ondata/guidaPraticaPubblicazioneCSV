---
hide:
 - toc
# - navigation
title: Linee guida per esportazione/importazione di dati tabulari da strumenti di foglio di calcolo a CSV
---

L'**esportazione diretta** in formato `CSV` da **Excel** o da **Libreoffice Calc** può causare **problemi** se le tabelle di dati contengono: celle unite, formule, macro, schede di espansione dati o altre caratteristiche derivate dall'applicazione delle funzionalità proprie di questi strumenti.

Per **esportare correttamente** i dati tabulari dagli strumenti di elaborazione dei fogli di calcolo, è necessario considerare le seguenti **linee guida**:

- il separatore di campo della guida è la virgola e il separatore decimale è il punto. Excel prende il separatore dalle impostazioni di Windows, non dal nome del formato: su un computer con impostazioni italiane il file può uscire con `;` e con la virgola nei decimali, e va convertito prima di pubblicarlo;
- non usare **celle unite**;
- non lasciare **righe e/o colonne vuote** tra i dati;
- controllare i **formati delle celle**: una formula esce con il valore calcolato, ma le celle escono come sono visualizzate, quindi un formato a 2 decimali arrotonda il dato e una data può uscire come `31/01/2023`. Prima di esportare, usa il formato Generale per i numeri, `aaaa-mm-gg` per le date e Testo per i codici.

Una buona pratica per **verificare** che i **dati esportati** siano formattati correttamente in `CSV` è quella di **aprire il file in un editor di testo** come Blocco note: deve esserci una riga per record, le lettere accentate devono essere leggibili (`città`, non `cittÃ `) e gli zeri iniziali devono esserci ancora (`082053`, non `82053`).

## Aprire un CSV in Excel senza rovinarlo

All'apertura di un CSV, Excel toglie gli zeri iniziali anche se il campo è tra virgolette, trasforma in date valori come `2023-07` e toglie il `+` dai numeri di telefono. Se Windows usa la virgola come separatore decimale, legge il punto come separatore delle migliaia: `1234.56` diventa `123456`, senza alcun avviso. Con un doppio clic, inoltre, un file separato da virgole può finire tutto in una sola colonna.

Per questo il doppio clic è sconsigliato. La procedura che lascia i valori integri è questa (nomi dei menu di Excel in inglese):

1. Data > From Text/CSV, e scegli il file.
2. In Data Type Detection scegli Do not detect data types.
3. Clicca Transform Data, poi Use First Row as Headers.
4. In Applied Steps elimina l'ultimo passaggio, Changed Type.
5. Clicca Close & Load.

Tutte le colonne restano testo: per farci calcoli vanno convertite dopo.

## Salvare un CSV da Excel

- si raccomanda di **esportare** i dati tabellari in formato **`CSV`** utilizzando la **codifica standard dei caratteri `UTF-8`**;
- il formato «CSV UTF-8» di Excel conserva tutti i caratteri e aggiunge il BOM. Meglio pubblicare il file senza BOM, ma un file che lo contiene non è sbagliato;
- il formato «CSV» semplice scrive in Windows-1252: `à` e `€` restano, mentre caratteri come `ł` o `日` diventano `?` e non si possono più recuperare;
- se la versione di Excel utilizzata non salva direttamente il file di dati codificato come `UTF-8`, è consigliabile **utilizzare una procedura di conversione di formato** che garantisca questa codifica di caratteri, ad esempio con LibreOffice Calc.
