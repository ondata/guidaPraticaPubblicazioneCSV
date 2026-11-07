---
hide:
 - toc
# - navigation
---

# Tipi di dati

Il CSV è testo e non contiene tipi: ogni valore va scritto in modo coerente con il [tipo di dati](https://www.w3.org/TR/xmlschema11-2/) dichiarato nel dizionario o nello schema.

| dato | tipo |
| --- | --- |
| Testo | string |
| Numero | integer, decimal, float, double |
| Data | date, time, dateTime, gYear, gYearMonth |
|Vero/Falso| boolean (`true`/`false`, oppure valori dichiarati nello schema) |

Da tenere in considerazione:

- Utilizzare un formato corretto per i campi, in base al tipo di dati che contengono, aumenta la probabilità che un'esportazione in altri formati abbia successo e rende i dati meglio utilizzabili.

### Esempio:
tipi di dati in tre colonne (string, integer, integer).

!!! failure "Cattiva prassi"

    | marca | consumo | potenza |
    | --- | --- | --- |
    | chevrolet chevelle malibu | 18 | 130 CV |
    | buick skylark 320 | 15 mpg | 165 |
    | plymouth satellite | 18 | 150 CV |
    | amc rebel sst | 16 mpg | 150 CV |
    | ford torino | 17 | 140 |

!!! success "Buona prassi"

    | marca | consumo_mpg | potenza_cv |
    | --- | ---: | ---: |
    | chevrolet chevelle malibu | 18 | 130 |
    | buick skylark 320 | 15 | 165 |
    | plymouth satellite | 18 | 150 |
    | amc rebel sst | 16 | 150 |
    | ford torino | 17 | 140 |

Se l'unità è la stessa per tutta la colonna, si indica nel nome (`consumo_mpg`, `potenza_cv`) e si ripete nel [dizionario dei dati](../dizionario_dati.md). Se pubblichi anche uno schema, descrivila lì: nel campo `description` di Table Schema puoi aggiungere dettagli che nel nome non ci stanno, come il codice dell'unità o la fonte. Se l'unità cambia da riga a riga, si usa una colonna dedicata subito dopo quella del valore.
