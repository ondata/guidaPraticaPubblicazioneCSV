---
hide:
# - toc
# - navigation
title: Campi di tipo numerico
---

# Campi di tipo numerico

I campi numerici devono essere codificati esclusivamente come tipi di dati numerici (interi o decimali). Se non si fa diversamente, alcune operazioni sui dati, come l'ordinamento, possono causare problemi inaspettati.

## In generale

  - Non si devono usare i **separatori delle migliaia** (quindi semplicemente `1230` e non `1.230`).
  - Il **separatore dei decimali** può essere una `,` o un `.`, a seconda della configurazione "locale" delle applicazioni di elaborazione dati e del sistema operativo. In Italia, Spagna, Francia o Germania, tra gli altri paesi, si usa la `,`, mentre nell'area anglosassone il `.`. L'uso dell'uno o dell'altro carattere, può comportare una pre elaborazione del dato, per quei linguaggi di programmazione o programmi in cui il separatore dei decimali è soltanto di un tipo.
  - I **valori negativi** devono essere preceduti da un segno meno `-`. In alcuni *software* in numeri negativi sono tra parentesi tonde; non usarle per rappresentare questo tipo di valori.
  - Se una colonna contiene sia valori interi che decimali, il tipo di dati deve essere decimale.
  - Se una colonna contiene solo valori interi, essi devono essere espressi senza separatore decimale.
  - **Non mescolare** nello stesso campo **testo** e **valori numerici**. Per esempio: non usare `€50` o `27%` come valore in un campo numerico, ma soltanto `50` o `27`.

## Valute
  - I valori numerici devono essere espressi senza decimali o con 2 decimali.
  - Il numero di cifre decimali utilizzato per formattare l'intera colonna di valori non deve variare. Se varia, la caratteristica di coerenza dei dati è violata.
  - **Non includere simboli di valuta** o separatori di migliaia (punti e virgole, a seconda dei casi).
## Unità di misura

  - Si deve usare il numero di decimali necessario.
  - Si raccomanda di usare il [dizionario dei dati](../dizionario_dati.md) per esprimere le unità di misura associate ai valori numerici. Se non c'è un dizionario, è possibile indicare l'unità di misura nel nome del campo, per esempio `distanza_metri`, purché tutti i valori della colonna abbiano la stessa unità di misura associata.
  - Nel caso in cui l'unità di misura sia diversa per una stessa colonna, i valori per ogni unità di misura devono essere indicati in una colonna separata da inserite subito dopo quella a cui fa riferimento.

Esempio:

| marca | prezzo_vendita | valuta |
| --- | --- | --- |
| chevrolet chevelle malibu | 23540,20 | EUR |
| buick skylark 320 | 22189,00 | EUR |
| plymouth satellite | 28362,65 | USD |
| amc rebel sst | 29200,00 | USD |

## Valori codificati

  - Quando ci sono degli zeri iniziali, devono  essere  digitati come valori di testo, quindi tra `"` (ad esempio `"0123"`), per evitare che il valore venga troncato e che ad esempio `00000023456` sia interpretato come `23456`.

## Esempi

**Esempio 1**: non usare i separatori di migliaia. Uso del separatore decimale. Coerenza nel numero di cifre decimali. Evitare di mescolare il testo con i valori numerici.

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

**Esempio 2**: : utilizzare il numero di decimali appropriato per ogni tipo di dato numerico. Usa il segno meno `-` per i valori negativi. Digita degli zeri significativi come valori di testo.

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

**Esempio 3**: cosa avviene quando si ordinano campi.

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

Una buona pratica è quella di controllare il tipo di dato prima della pubblicazione, o nel sistema/programma in cui viene generato il file, o con uno degli strumenti di convalida della sezione "[Strumenti per i file CSV](../strumenti_file_CSV.md)".
