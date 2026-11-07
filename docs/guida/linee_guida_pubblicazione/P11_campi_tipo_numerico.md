---
hide:
- toc
# - navigation
title: Scrivi i numeri con il punto decimale
---

# 11. Scrivi i numeri con il punto decimale

In una colonna di numeri devono esserci solo numeri: il punto come separatore decimale (`8200.50`), nessun separatore delle migliaia, nessun simbolo o parola accanto al valore. L'unità di misura sta nel nome della colonna.

## Così sì e così no

Nomi delle biblioteche, importi e prestiti di questa pagina sono inventati.

!!! failure "Così no"

    | biblioteca | spesa_acquisti |
    | --- | --- |
    | Biblioteca di esempio A | 8.200,50 |
    | Biblioteca di esempio B | 1250,00 € |
    | Biblioteca di esempio C | 300 euro |
    | Biblioteca di esempio D | 15,400.75 |

!!! success "Così sì"

    | biblioteca | spesa_acquisti_euro |
    | --- | ---: |
    | Biblioteca di esempio A | 8200.50 |
    | Biblioteca di esempio B | 1250.00 |
    | Biblioteca di esempio C | 300.00 |
    | Biblioteca di esempio D | 15400.75 |

Aperte con un editor di testo, le stesse righe si leggono così:

```csv
biblioteca,spesa_acquisti_euro
Biblioteca di esempio A,8200.50
Biblioteca di esempio B,1250.00
Biblioteca di esempio C,300.00
Biblioteca di esempio D,15400.75
```

## Perché

Chi riusa i dati vuole sommare, ordinare e filtrare, per esempio tutte le biblioteche che spendono più di 1000 euro. Se nella colonna c'è anche un solo `300 euro`, un programma può leggere tutta la colonna come testo, e somme e filtri non funzionano.

Il punto è il valore predefinito di CSV on the Web (CSVW) e di Table Schema, e nel file non cambia con le impostazioni di chi legge. La virgola separa già le colonne: `8200,50` senza virgolette diventa due celle.

L'ordinamento mostra la differenza. Queste sono le stesse righe, ordinate per `prestiti`.

Se la colonna è letta come numeri, l'ordine è quello atteso:

| biblioteca | prestiti |
| --- | ---: |
| Biblioteca di esempio B | 3120 |
| Biblioteca di esempio A | 12450 |
| Biblioteca di esempio D | 20310 |

Se è letta come testo, il confronto va carattere per carattere, come in un dizionario: `3120` finisce dopo `20310` perché `3` viene dopo `2`.

| biblioteca | prestiti |
| --- | --- |
| Biblioteca di esempio A | 12450 |
| Biblioteca di esempio D | 20310 |
| Biblioteca di esempio B | 3120 |

## Casi particolari

- **Valori negativi**: si scrivono con il segno meno, `-120.50`. Alcuni programmi mostrano i negativi tra parentesi tonde: nel file non vanno usate.
- **Solo numeri interi**: si scrivono senza separatore decimale, `12450` e non `12450.00`.
- **Interi e decimali nella stessa colonna**: la colonna è decimale. Il numero di decimali dipende da che cosa si misura e dallo strumento usato per misurarlo.

### Valute

Un importo ha i decimali previsti dalla valuta secondo la norma ISO 4217: 2 per l'euro, 0 per lo yen, 3 per il dinaro kuwaitiano ([elenco ISO 4217](https://www.six-group.com/en/products-services/financial-information/market-reference-data/data-standards.html)). Se la valuta è una sola, il numero di decimali non deve variare nella colonna. Niente simboli di valuta né separatori delle migliaia.

Il codice di valuta sta nel dizionario dei dati (`EUR`) se la valuta è una sola. Se le valute sono più di una sta in una colonna, subito dopo quella del valore, e ogni riga ha i decimali della sua valuta:

| biblioteca | spesa_acquisti | valuta |
| --- | ---: | --- |
| Biblioteca di esempio A | 8200.50 | EUR |
| Biblioteca di esempio B | 1250.00 | USD |
| Biblioteca di esempio C | 45000 | JPY |

### Percentuali

Scrivi `27`, non `27%`. Il simbolo non va nella cella, ma va dichiarata nel [dizionario dei dati](../dizionario_dati.md) la scala della colonna: `27` se va da 0 a 100, oppure `0.27` se va da 0 a 1.

### Unità di misura

Si usa il numero di decimali necessario. Se l'unità è la stessa per tutta la colonna, si indica nel nome (`spesa_acquisti_euro`, `distanza_metri`) e si ripete nel [dizionario dei dati](../dizionario_dati.md). Se pubblichi anche uno schema, descrivila lì: nel campo `description` di Table Schema puoi aggiungere dettagli che nel nome non ci stanno, come il codice dell'unità o la fonte.

Se l'unità cambia da riga a riga, si usa una colonna dedicata, subito dopo quella del valore. I codici si possono prendere dalla tabella delle unità di misura delle [EU Vocabularies](https://op.europa.eu/en/web/eu-vocabularies/authority-tables).

### Codici fatti di cifre

I codici fatti di cifre sono testo, non numeri: vedi la scheda sui [codici](P09_campi_codificati.md).

## Come si fa nel foglio di calcolo

!!! warning "Excel e il punto decimale"

    Un Excel con impostazioni italiane può leggere `1234.56` come `123456`, senza avviso. Prima di aprire un CSV leggi [come aprire un CSV in Excel](Linee_guida_importazione_esportazione.md#aprire-un-csv-in-excel-senza-rovinarlo).

- Non riscrivere i numeri a mano nel foglio: lì restano nel formato del tuo computer. Il punto decimale riguarda il file CSV, e ci arriva con la [conversione](Linee_guida_importazione_esportazione.md#convertire-in-csv-con-libreoffice-calc).
- Nel foglio, prima di esportare, usa il formato Generale per i numeri e un formato a 2 decimali per gli importi: le celle escono come sono visualizzate, quindi un formato con meno decimali del dato lo arrotonda.
- Se il file esce con `;` e la virgola nei decimali, va [convertito con LibreOffice Calc](Linee_guida_importazione_esportazione.md#convertire-in-csv-con-libreoffice-calc) prima di pubblicarlo.
- Nella conversione con LibreOffice Calc il formato `General` toglie gli zeri finali: `1250.00` diventa `1250`. Per gli importi usa il formato `0.00` indicato [nella stessa pagina](Linee_guida_importazione_esportazione.md#convertire-in-csv-con-libreoffice-calc), così la colonna conserva lo stesso numero di decimali.
- Controlla il tipo di dato prima di pubblicare, nel programma che genera il file o con uno degli strumenti della [strumenti di controllo](Cassetta_attrezzi.md).

Vedi anche: [7. Un solo tipo di dato per colonna](P07_tipi_dati.md), [9. Affianca una descrizione ai codici](P09_campi_codificati.md), [15. Scrivi le coordinate in gradi decimali](P15_campi_con_coordinate_geografiche.md).
