---
hide:
# - toc
# - navigation
title: Benvenute/i
---


Le serie di **dati tabellari** ben organizzate, conformi a uno schema predefinito, sono facili da manipolare, modellare e visualizzare, e hanno una struttura specifica basata sulle seguenti regole:

- Ogni variabile è una **colonna**.
- Ogni osservazione è una **riga**.
- Ogni intersezione di riga e colonna è una **cella**.
- Ogni serie di osservazioni è una **tabella**.

!!! example "Caratteristiche delle auto d'epoca"

    | marca | anno | cilindri | consumo | potenza | accelerazione |
    | --- | --- | --- | --- | --- | --- |
    | chevrolet chevelle malibu | 1970 | 8 | 18 | 130 | 12 |
    | buick skylark 320 | 1970 | 8 | 15 | 165 | 11.5 |
    | plymouth satellite | 1970 | 8 | 18 | 150 | 11 |
    | amc rebel sst | 1970 | 8 | 16 | 150 | 12 |
    | ford torino | 1970 | 8 | 17 | 140 | 10.5 |

Anche se non esiste uno standard ufficiale per il formato "Comma Separated Values" (CSV), l'*Internet Engineering Task Force* (IETF) pubblica il documento di riferimento [RFC4180](https://tools.ietf.org/html/rfc4180).

## Caratteristiche principali

- Ogni file deve contenere solo una tabella di dati.
- Ogni record o riga è una linea.
- Tutti i record contengono lo stesso numero di campi o colonne, almeno uno.
- Facoltativamente, ci può essere una prima riga di intestazione contenente solo i nomi dei campi.
- Le celle nella stessa colonna forniscono valori per la stessa proprietà delle osservazioni descritte in ciascuna riga.
- Tutti i valori nella stessa colonna devono essere dello stesso tipo di dati (testo, intero, decimale, data, ecc.).
- Ogni campo è separato dal successivo da un singolo carattere: per esempio, una virgola `,`, un punto e virgola `;`, un carattere *pipe* `|` o un carattere di tabulazione `TAB`.
- Quando i campi sono separati da un carattere di tabulazione `TAB`, il formato del file è [**TSV**](https://www.iana.org/assignments/media-types/text/tab-separated-values).
- In alternativa, i campi possono avere una lunghezza fissa di caratteri.
- I valori dei campi che includono virgolette, virgole o ritorni a capo devono essere racchiusi tra virgolette.
- I file in formato CSV devono utilizzare la codifica dei caratteri `UTF-8`.
- Per quanto riguarda i nomi dei file, si raccomanda di usare lettere minuscole con i caratteri a-z, le cifre 0-9 e l'underscore (`_`) invece degli spazi bianchi, per assicurare la corretta elaborazione dei nomi dei file sia sui server che sulle applicazioni client.
- Qualsiasi informazione diversa dai valori dei dati, come metadati, descrizioni, commenti o unità di misura, deve essere fornita come allegato al file di dati sotto forma di dizionario dei dati.

## Esempio di file CSV

```
marca,anno,cilindri,consumo,potenza,accelerazione
chevrolet chevelle malibu,1970,8,18,130,12
buick skylark 320,1970,8,15,165,11.5
plymouth satellite,1970,8,18,150,11
amc rebel sst,1970,8,16,150,12
ford torino,1970,8,17,140,10.5
```

