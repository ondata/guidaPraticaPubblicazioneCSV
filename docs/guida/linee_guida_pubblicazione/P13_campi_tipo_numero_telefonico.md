---
hide:
- toc
# - navigation
title: Campi con numeri telefonici
---

# Campi con numeri telefonici

È consigliato scrivere i numeri nel formato internazionale, senza spazi né trattini: `+390515270001`, cioè `+`, il prefisso del Paese e il numero. La colonna è di testo. Per i numeri interni si usa una colonna a parte.

Excel e LibreOffice possono togliere il `+` quando aprono il file: per conservarlo importa la colonna come testo, e non salvare il file dopo averlo aperto con un doppio clic.

Da prendere in considerazione:

- quando è necessario includere **più di un numero di telefono**, è necessario utilizzare **un campo per ogni numero**, ad esempio `ufficio` e `mobile`;
- per i numeri di telefono che richiedono l'inclusione di un **numero interno**, si dovrebbe considerare la creazione di un **campo specifico**, ad esempio `numero_interno`, questo campo potrebbe contenere caratteri non numerici come `*86`, `#36` e dovrebbe essere un **campo di testo**.


### Esempio:

tabella con una colonna che contiene numeri di telefono

!!! failure "Cattiva prassi"

    | marchio | telefono_rivenditore |
    | --- | --- |
    | chevrolet chevelle malibu | +39-0510000001 |
    | buick skylark 320 | (39)0510000002 |
    | plymouth satellite | 39-051-000-0003 |
    | amc rebel sst | 0510000004 |

!!! success "Buona prassi"

    | marchio | telefono_rivenditore |
    | --- | --- |
    | chevrolet chevelle malibu | +390510000001 |
    | buick skylark 320 | +390510000002 |
    | plymouth satellite | +390510000003 |
    | amc rebel sst | +390510000004 |
