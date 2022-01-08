---
hide:
 - toc
# - navigation
---

# Tipi di dati

I valori in una tabella di dati devono essere formattati secondo il [tipo di dati](https://www.w3.org/TR/xmlschema/) relativo. In particolare, i numeri dovrebbero essere sempre nei formati/tipi di cella "Numero", i campi di tipo testo dovrebbero essere nel formato/tipo di cella "Testo" e i campi di tipo data dovrebbero essere nel formati/tipi di cella 'Data'.

| Dato | Tipo |
| --- | --- |
| Testo | string |
| Numero | integer, decimal, float, double |
| Data | date, time, datetime, Year, Month, Day |
|Vero/Falso| boolean |

Da tenere in considerazione:

- Utilizzare un formato corretto per i campi, in base al tipo di dati che contengono, aumenta la probabilità che un'esportazione in altri formati abbia successo e rende i dati più utilizzabili.

**Esempio**: tipi di dati in tre colonne (string, integer, integer).

!!! failure "Cattiva prassi"

    | marca | consumo | potenza |
    | --- | --- | --- |
    | chevrolet chevelle malibu | 18 | 130 CV |
    | buick skylark 320 | 15 litri | 165 |
    | plymouth satellite | 18 | 150 CV |
    | amc rebel sst | 16 l. | 150 CV |
    | ford torino | 17 | 140 |

!!! success "Buona prassi"

    | marca | consumo | potenza |
    | --- | ---: | ---: |
    | chevrolet chevelle malibu | 18 | 130 |
    | buick skylark 320 | 15 | 165 |
    | plymouth satellite | 18 | 150 |
    | amc rebel sst | 16 | 150 |
    | ford torino | 17 | 140 |

La buona pratica indica che le unità di misura dovrebbero essere descritte nel [dizionario dei dati](../dizionario_dati.md) e non nella denominazione dei campi, o come valori delle celle. Come ultima risorsa, se non c'è un dizionario, è possibile indicare l'unità di misura nel nome del campo, per esempio `consumo_litri` o `potenza_cv`, purché tutti i valori della colonna abbiano la stessa unità di misura associata.
