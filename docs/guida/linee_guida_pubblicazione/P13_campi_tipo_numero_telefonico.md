---
hide:
- toc
# - navigation
title: Campi con numeri telefonici
---

# Campi con numeri telefonici

Quando si includono **valori con numeri di telefono**, la cosa più importante è assicurare la **coerenza del formato** di questi numeri in tutti i valori della colonna, è possibile usare `+39-0515270001` o `(39)0515270001` o anche `39-051-527-0001`, ma l'importante è **utilizzare sempre lo stesso formato**.

Da prendere in considerazione:

- quando è necessario includere **più di un numero di telefono**, è necessario utilizzare **un campo per ogni numero**, ad esempio `ufficio` e `mobile`;
- è consigliato **includere il prefisso del paese** prima del numero di telefono, per l'Italia `+39` oppure `0039`;
- per i numeri di telefono che richiedono l'inclusione di un **numero interno**, si dovrebbe considerare la creazione di un **campo specifico**, ad esempio `numero_interno`, questo campo potrebbe contenere caratteri non numerici come `*86`, `#36` e dovrebbe essere un **campo di testo**.


### Esempio:

tabella con una colonna che contiene numeri di telefono

!!! failure "Cattiva prassi"

    | marchio | telefono_rivenditore |
    | --- | --- |
    | chevrolet chevelle malibu | +34-6760000 |
    | buick skylark 320 | (34)6960001 |
    | plymouth satellite | 34-676-00-03 |
    | amc rebel sst | 346960004 |

!!! success "Buona prassi"

    | marchio | telefono_rivenditore |
    | --- | --- |
    | chevrolet chevelle malibu | +34-6760000 |
    | buick skylark 320 | +34-6960001 |
    | plymouth satellite | +34-6760003 |
    | amc rebel sst | +34-6960004 |
