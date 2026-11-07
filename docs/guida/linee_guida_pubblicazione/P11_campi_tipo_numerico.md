---
hide:
- toc
# - navigation
title: Campi di tipo numerico
---

# Campi di tipo numerico

I campi numerici devono essere codificati esclusivamente come tipi di dati numerici (interi o decimali); se si fa diversamente, alcune operazioni sui dati come l'ordinamento, il filtraggio (tutte le righe in cui i valori di una colonna sono superiori a una certa cifra), possono non funzionare e/o produrre risultati inattesi.

## In generale:

  - non si devono usare i **separatori delle migliaia** (quindi semplicemente `1230` e non `1.230`);
  - il **separatore dei decimali** è il punto (`1234.56`): è il valore predefinito di CSVW e di Table Schema, e nel file non cambia con le impostazioni di chi legge. Attenzione: un Excel con impostazioni italiane può leggere `1234.56` come `123456`, vedi [come aprire un CSV in Excel](Linee_guida_importazione_esportazione.md);
  - i **valori negativi** devono essere preceduti da un segno meno `-`; in alcuni *software* i numeri negativi sono tra parentesi tonde, non usarle per rappresentare questo tipo di valori;
  - se una colonna contiene sia valori **interi** che **decimali**, il **tipo di dati** deve essere **decimale** e deve essere inserito il numero corretto di cifre decimali (che può dipendere dall'entità misurata, dalla strumentazione usata per raccogliere quei valori, ecc.);
  - se una colonna contiene **solo valori interi**, essi devono essere espressi **senza separatore decimale**;
  - **non mescolare** nello stesso campo **testo** e **valori numerici**, per esempio: non usare `€50` o `27%` come valore in un campo numerico, ma soltanto `50` o `27`.

## Valute:

  - i valori numerici devono essere espressi senza decimali o con 2 decimali;
  - il numero di cifre decimali utilizzato per formattare l'intera colonna di valori non deve variare, se varia, la caratteristica di coerenza dei dati è violata;
  - **non includere simboli di valuta** o separatori di migliaia.

## Unità di misura:

  - si deve usare il **numero di decimali necessario**;
  - se l'**unità di misura** è la stessa per tutta la colonna, si indica nel nome (per esempio `distanza_metri`) e si ripete nel [dizionario dei dati](../dizionario_dati.md). Se pubblichi anche uno schema, descrivila lì: nel campo `description` di Table Schema puoi aggiungere dettagli che nel nome non ci stanno, come il codice dell'unità o la fonte;
  - se l'**unità di misura** cambia da riga a riga, si usa una **colonna dedicata**, subito dopo quella del valore. I codici si possono prendere dalla tabella delle unità di misura delle [EU Vocabularies](https://op.europa.eu/en/web/eu-vocabularies/authority-tables).

!!! info "UNECE Units of measure"

    La Commissione economica per l'Europa delle Nazioni Unite (UNECE) gestisce il dataset "[UNECE Units of measure](https://datahub.io/core/unece-units-of-measure)" in     cui vengono definiti dei codici standard introdotti dalla Recommendation 20 al fine di rappresentare unità di misura di grandezze fisiche e non.

### Esempio:

| marca | prezzo_vendita | valuta |
| --- | ---: | --- |
| chevrolet chevelle malibu | 23540.20 | EUR |
| buick skylark 320 | 22189.00 | EUR |
| plymouth satellite | 28362.65 | USD |
| amc rebel sst | 29200.00 | USD |

## Valori codificati

Spesso i [campi codificati](P09_campi_codificati.md) sono composti esclusivamente da stringhe numeriche, ma non sono né numeri interi, né decimali: ad esempio un numero di telefono come `081292240`.<br>
In questi casi, specie in presenza di uno o più `0` a inizio cella, il campo deve essere impostato come campo di testo e eventualmente dichiarato come tale nel [dizionario dei dati](../dizionario_dati.md), questo per evitare che il valore venga interpretato come numero e troncato (ad esempio da `081292240` a `81292240`).

### Esempio 1:
non usare i separatori di migliaia, uso del separatore decimale, coerenza nel numero di cifre decimali, evitare di mescolare il testo con i valori numerici.

!!! failure "Cattiva prassi"

    | marca | ricavi_vendite |
    | --- | --- |
    | chevrolet chevelle malibu | 1.234.454,34 € |
    | buick skylark 320 | 2.345.567,89 euro |
    | plymouth satellite | 344,678.23 |
    | amc rebel sst | 267.331 |
    | ford torino | 1.234678.67 |

!!! success "Buona prassi"

    | marca | ricavi_vendite_euro |
    | --- | ---: |
    | chevrolet chevelle malibu | 1234454.34 |
    | buick skylark 320 | 2345567.89 |
    | plymouth satellite | 344678.23 |
    | amc rebel sst | 267331.00 |
    | ford torino | 1234678.67 |

In questo esempio la valuta è la stessa per tutti i valori, quindi è nel nome del campo e si ripete nel dizionario dei dati.

### Esempio 2:
utilizzare il numero di decimali appropriato per ogni tipo di dato numerico, usare il segno meno `-` per i valori negativi, trattare come testo i valori con zeri iniziali che contano.

!!! failure "Cattiva prassi"

    | identificatore_di_marca | punto_chilometrico | latitudine | longitudine |
    | --- | --- | --- | --- |
    | 345600 | 2.3 | 43,2345678 | (5,1234567) |
    | 0000345601 | 12,56 | 43,345 | -5,2345678 |

!!! success "Buona prassi"

    | identificatore_di_marca | punto_chilometrico | latitudine | longitudine |
    | --- | ---: | ---: | ---: |
    | 0000345600 | 2.3 | 43.2345678 | -5.1234567 |
    | 0000345601 | 12.56 | 43.345 | -5.2345678 |

### Esempio 3:
cosa avviene quando si ordinano campi.

Se il campo da ordinare contiene valori numerici, ed è impostato come tipo di dato numerico, sarà possibile ordinarlo numericamente in modo corretto.

Tabella di input:

| marca | classifica |
| --- | ---: |
| chevrolet chevelle malibu | 1 |
| buick skylark 320 | 9 |
| plymouth satellite | 6 |
| amc rebel sst | 2 |
| ford torino | 4 |

Output dopo ordinamento per colonna `classifica`:

| marca | classifica |
| --- | ---: |
| chevrolet chevelle malibu | 1 |
| amc rebel sst | 2 |
| ford torino | 4 |
| plymouth satellite | 6 |
| buick skylark 320 | 9 |

Se invece il campo da ordinare contiene valori numerici, ma è impostato come semplice testo, l'ordinamento numerico sarà scorretto.

Tabella di input:

| marca | classifica |
| --- | --- |
| chevrolet chevelle malibu | "123" |
| buick skylark 320 | "9" |
| plymouth satellite | "324" |
| amc rebel sst | "11" |
| ford torino | "45" |

Output dopo ordinamento per colonna `classifica`:

| marca | classifica |
| --- | --- |
| amc rebel sst | "11" |
| chevrolet chevelle malibu | "123" |
| plymouth satellite | "324" |
| ford torino | "45" |
| buick skylark 320 | "9" |

In quest'ultimo esempio, le virgolette `"` intorno ad ogni stringa di numeri sono incluse per rendere l'esempio più esplicito, ma in un foglio elettronico reale non sono visibili anche se il campo è di tipo "testo".

Una buona pratica è quella di **controllare il tipo di dato prima della pubblicazione**, o nel sistema/programma in cui viene generato il file, o con uno degli strumenti di convalida della sezione [Cassetta degli attrezzi per i file CSV](Cassetta_attrezzi.md).
