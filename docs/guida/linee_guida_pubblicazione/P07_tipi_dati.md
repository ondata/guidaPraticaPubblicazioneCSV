---
hide:
 - toc
# - navigation
title: Un solo tipo di dato per colonna
---

# 7. Un solo tipo di dato per colonna

Ogni colonna deve contenere un solo tipo di dato: solo numeri, solo date oppure solo testo, come dichiarato nel [dizionario dei dati](../dizionario_dati.md). L'unità di misura deve stare nel nome della colonna, non nelle celle.

## Così sì e così no

Nomi delle biblioteche e importi sono inventati. In questa colonna alcune celle contengono un numero, altre un numero seguito da testo.

!!! failure "Così no"

    | biblioteca | anno | spesa_acquisti |
    | --- | ---: | --- |
    | Biblioteca di esempio A | 2023 | 8200.50 |
    | Biblioteca di esempio B | 2023 | 1250.00 euro |
    | Biblioteca di esempio C | 2023 | 300.00 |
    | Biblioteca di esempio D | 2023 | 15400.75 euro |

!!! success "Così sì"

    | biblioteca | anno | spesa_acquisti_euro |
    | --- | ---: | ---: |
    | Biblioteca di esempio A | 2023 | 8200.50 |
    | Biblioteca di esempio B | 2023 | 1250.00 |
    | Biblioteca di esempio C | 2023 | 300.00 |
    | Biblioteca di esempio D | 2023 | 15400.75 |

## Perché

Il CSV è testo e non contiene tipi: a dire che una colonna è numerica sono solo i valori scritti in modo coerente con il dizionario. Un foglio di calcolo legge `1250.00 euro` come testo e la somma lo salta: nel primo esempio la spesa risulta 8500.50 invece di 25151.25, senza alcun avviso.

## Casi particolari

- **Unità uguale per tutta la colonna.** Si indica nel nome (`spesa_acquisti_euro`) e si ripete nel [dizionario dei dati](../dizionario_dati.md).
- **Unità che cambia da riga a riga.** Si usa una colonna dedicata, subito dopo quella del valore.
- **Valore mancante.** La cella vuota non cambia il tipo della colonna: `prestiti` resta una colonna di numeri interi anche se per una biblioteca il dato non c'è.
- **Codici fatti di cifre.** Sono testo, non numeri: dichiara `082053` come testo.

### Se pubblichi anche uno schema

Uno schema è un file che descrive le colonne in una forma che i programmi sanno leggere. Descrivi lì anche l'unità: nel campo `description` di Table Schema puoi aggiungere dettagli che nel nome non ci stanno, come il codice dell'unità o la fonte.

I tipi hanno nomi diversi a seconda del formato: Table Schema ha i propri, CSVW (CSV on the Web) usa quelli di [XML Schema](https://www.w3.org/TR/xmlschema11-2/). Nel dizionario basta la prima colonna della tabella.

| Dato | Esempio | Table Schema | XML Schema |
| --- | --- | --- | --- |
| Testo | `Roma` | `string` | `string` |
| Numero intero | `12450` | `integer` | `integer` |
| Numero decimale | `8200.50` | `number` | `decimal`, `float`, `double` |
| Data | `1985-03-12` | `date` | `date` |
| Ora | `15:10:00` | `time` | `time` |
| Data e ora | `1970-01-12T15:10:00` | `datetime` | `dateTime` |
| Anno | `2023` | `year` | `gYear` |
| Anno e mese | `2023-07` | `yearmonth` | `gYearMonth` |
| Vero o falso | `true`, oppure valori dichiarati nello schema | `boolean` | `boolean` |

Vedi anche: [3. Nomi di colonna chiari](P03_denominazione_colonne.md), [5. Se un valore manca, lascia la cella vuota](P05_trattamento_valori_sconosciuti.md), [9. Affianca una descrizione ai codici](P09_campi_codificati.md), [11. Scrivi i numeri con il punto decimale](P11_campi_tipo_numerico.md), [12. Scrivi le date come AAAA-MM-GG](P12_campi_tipo_data.md).
