---
hide:
- toc
# - navigation
title: Campi di tipo data
---

# Campi di tipo data

Codificare le **date** utilizzando uno **standard** è fondamentale per facilitare l'analisi dei dati delle serie temporali. Lo standard di riferimento è quello definito dalla norma [ISO8601](https://es.wikipedia.org/wiki/ISO_8601), che codifica i valori di data con il formato `YYYYY-MM-DD`, nella sua forma abbreviata, o `YYYYY-MM-DDTHH:MM:SS`, nella sua versione estesa.

## Date:

Nel caso delle date è utile utilizzare le seguenti raccomandazioni

- Riempite di zeri i valori 0-9 per indicare MM, DD, HH, MM e SS, poich  ogni valore deve avere un numero fisso di cifre.
- Usa "-" come separatore per le date e ":" per le ore.
- Usa la lettera "T" come carattere separatore tra una data e un'ora quando usi la versione estesa.
- preferibile usare le date complete (AAAA-MM-GG) piuttosto che indicare solo i mesi o gli anni, quando ci    possibile dalla fonte dei dati.
- Se sono disponibili solo dati mensili, l'opzione migliore   quella di includere una data completa aggiustata all'ultimo giorno del mese. Per esempio, per settembre, 2019-09-30.
- Se la data completa non pu  essere inclusa,   preferibile esprimere anno e mese in colonne separate.   persino ragionevole includere una colonna per indicare il nome del mese.



  

### Esempio:

| marca | prezzo_vendita | valuta |
| --- | --- | --- |
| chevrolet chevelle malibu | 23540,20 | EUR |
| buick skylark 320 | 22189,00 | EUR |
| plymouth satellite | 28362,65 | USD |
| amc rebel sst | 29200,00 | USD |

## Valori codificati

Spesso i [campi codificati](P09_campi_codificati.md) sono composti esclusivamente da stringhe numeriche, ma non sono né numeri interi, né decimali: ad esempio un numero di telefono come `081292240`.<br>
In questi casi, specie in presenza di uno o più `0` a inizio cella, il campo deve essere impostato come campo di testo e eventualmente dichiarato come tale nel [dizionario dei dati](../dizionario_dati.md), questo per evitare che il valore venga interpretato come numero e troncato (ad esempio da `081292240` a `81292240`).

### Esempio 1:
non usare i separatori di migliaia, uso del separatore decimale, coerenza nel numero di cifre decimali, evitare di mescolare il testo con i valori numerici.

!!! failure "Cattiva prassi"

    | marca | ricavi_vendite |
    | --- | --- |
    | chevrolet chevelle malibu | 1.234.454,34 € |
    | buick skylark 320 | 2.345.567,892 euro |
    | plymouth satellite | 344,678.23 |
    | amc rebel sst | 267.331 |
    | ford torino | 1.234678.67 |

!!! success "Buona prassi"

    | marca | ricavi_vendite |
    | --- | --- |
    | chevrolet chevelle malibu | 1234454,34 |
    | buick skylark 320 | 2345567,89 |
    | plymouth satellite | 344678,23 |
    | amc rebel sst | 267331,00 |
    | ford torino | 1234678,67 |

In questo esempio, la valuta usata per tutti i valori nel campo `ricavi_vendite` è la stessa e sarà descritta nel dizionario dei dati. In alternativa, il nome del campo potrebbe essere `ricavi_vendite_euro`.

### Esempio 2:
utilizzare il numero di decimali appropriato per ogni tipo di dato numerico, usa il segno meno `-` per i valori negativi, digita degli zeri significativi come valori di testo.

!!! failure "Cattiva prassi"

    | identificatore_di_marca | punto_chilometrico | latitudine | longitudine |
    | --- | --- | --- | --- |
    | 345600 | 2.3 | 43,2345678 | (5,1234567) |
    | 0000345601 | 12,56 | 43,345 | -5,2345678 |

!!! success "Buona prassi"

    | identificatore_di_marca | punto_chilometrico | latitudine | longitudine |
    | --- | --- | --- | --- |
    | 0000345600 | 2,334 | 43,2345678 | -5,1234567 |
    | 0000345601 | 12,567 | 43,3456789 | -5,2345678 |

### Esempio 3:
cosa avviene quando si ordinano campi.

Se il campo da ordinare contiene valori numerici, ed è impostato come tipo di dato numerico, sarà possibile ordinarlo numericamente in modo corretto.

Tabella di input:

| marca | classifica |
| --- | --- |
| chevrolet chevelle malibu | 1 |
| buick skylark 320 | 9 |
| plymouth satellite | 6 |
| amc rebel sst | 2 |
| ford torino | 4 |

Output dopo ordinamento per colonna `classifica`:

| marca | classifica |
| --- | --- |
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

Una buona pratica è quella di **controllare il tipo di dato prima della pubblicazione**, o nel sistema/programma in cui viene generato il file, o con uno degli strumenti di convalida della sezione [strumenti per i file CSV](../strumenti_file_CSV.md).
