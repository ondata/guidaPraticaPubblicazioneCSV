---
hide:
 - toc
# - navigation
title: Linee guida per esportazione/importazione di dati tabulari da strumenti di foglio di calcolo a CSV
---

L'**esportazione diretta** in formato `CSV` da **Excel** o da **Libreoffice Calc** può causare **problemi** se le tabelle di dati contengono: celle unite, formule, macro, schede di espansione dati o altre caratteristiche derivate dall'applicazione delle funzionalità proprie di questi strumenti.

Per **esportare correttamente** i dati tabulari dagli strumenti di elaborazione dei fogli di calcolo, è necessario considerare le seguenti **linee guida**:

- in funzione seconda delle **impostazioni regionali** utilizzate sul proprio **computer**, può essere conveniente usare `;` o `|` (pipe) come **separatore di campo** piuttosto che `,` che in Europa è usata come separatore decimale;
- non usare **celle unite**;
- non lasciare **celle**, righe e/o colonne **vuote** tra i dati;
- non usare **campi calcolati**.

Una buona pratica per **verificare** che i **dati esportati** siano formattati correttamente in `CSV` è quella di **aprire il file in un editor di testo** come notepad, se l'esportazione è avvenuta correttamente, vedrai i dati esportati esattamente come formattati dal software di esportazione.

Quando **Excel importa dati `CSV`**, se i campi non sono racchiusi tra virgolette, **rimuove gli zeri iniziali** dai campi prima di visualizzarli; questo può causare problemi quando, per esempio, questi campi contengono chiavi numeriche, **rimuove** inoltre sempre **gli spazi iniziali**.

Alcune indicazioni:

- si raccomanda di **esportare** i dati tabellari in formato **`CSV`** utilizzando la **codifica standard dei caratteri `UTF-8`**;
- i **fogli di calcolo Excel**, che contengono alcuni **simboli speciali**, come la lettera `à`, l'accento `'`, la tilde `~` o altri caratteri speciali, possono causare **problemi durante l'esportazione** in CSV e il successivo recupero, perché il comando `Salva come CSV` distorce qualsiasi carattere non `ASCII`[^1];
- se la versione di Excel utilizzata non salva direttamente il file di dati codificato come `UTF-8`, è consigliabile **utilizzare una procedura di conversione di formato** che garantisca questa codifica di caratteri, oltre ad Excel (dalla versione 16 in poi), strumenti utili per questo compito sono Google Spreadsheet e LibreOffice Calc.

[^1]: [ASCII American Standard Code for Information Interchange](https://it.wikipedia.org/wiki/ASCII)