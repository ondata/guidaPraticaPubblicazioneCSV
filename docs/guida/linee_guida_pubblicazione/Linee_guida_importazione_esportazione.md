---
hide:
 - toc
# - navigation
title: Linee guida per esportazione/importazione di dati tabulari da strumenti di foglio di calcolo a CSV
---

L'**esportazione diretta** in formato `CSV` da **Excel** o da **Libreoffice Calc** può causare **problemi** se le tabelle di dati contengono: celle unite, formule, macro, schede di espansione dati o altre caratteristiche derivate dall'applicazione delle funzionalità proprie di questi strumenti.

Per **esportare correttamente** i dati tabulari dagli strumenti di elaborazione dei fogli di calcolo, è necessario considerare le seguenti **linee guida**:

- in funzione seconda delle **impostazioni regionali** utilizzate sul proprio **computer**, può essere conveniente usare `;` o pipe `|` come **separatore di campo** piuttosto che `,` che in Europa è usata come separatore decimale;
- non usare **celle unite**;
- non lasciare **celle**, righe e/o colonne **vuote** tra i dati;
- non usare **campi calcolati**.

Una buona pratica per **verificare** che i **dati esportati** siano formattati correttamente in `CSV` è quella di **aprire il file in un editor di testo** come notepad, se l'esportazione è avvenuta correttamente vedrai i dati esportati esattamente come formattati dal software di esportazione.

**TO DO**

- Quando Excel importa dati CSV, rimuove gli zeri iniziali dai campi prima di visualizzarli, se i campi non sono racchiusi tra virgolette. Questo pu  causare problemi quando, per esempio, questi campi contengono chiavi numeriche. Inoltre, rimuovete sempre gli spazi iniziali.
- Si raccomanda di esportare i dati tabellari in formato CSV utilizzando la codifica standard dei caratteri UTF-8.
- I fogli di calcolo Excel che contengono alcuni simboli speciali, come la lettera " ", gli accenti, gli accenti, ecc. o altri caratteri speciali, possono causare problemi durante l'esportazione in CSV e il successivo recupero, perch  il comando "Save as CSV" distorce qualsiasi carattere non-ASCII.
- Se la versione di Excel utilizzata non salva direttamente il file di dati codificato come UTF-8,   consigliabile utilizzare una procedura di conversione di formato che garantisca questa codifica di caratteri. Oltre a Excel (dalla versione 16 in poi), strumenti utili per questo compito sono Google Spreadsheet e LibreOffice Calc.