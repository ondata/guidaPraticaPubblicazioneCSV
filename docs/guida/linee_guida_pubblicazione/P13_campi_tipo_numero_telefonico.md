---
hide:
- toc
# - navigation
title: Scrivi i telefoni in formato internazionale
---

# 13. Scrivi i telefoni in formato internazionale

È consigliato scrivere i numeri nel formato internazionale, senza spazi né trattini: `+390910000001`, cioè `+`, il prefisso del Paese e il numero. La colonna è di testo.

## Così sì e così no

Nomi delle biblioteche e numeri di telefono di questa pagina sono inventati. Se il numero manca, la cella resta vuota.

!!! failure "Così no"

    | biblioteca | telefono |
    | --- | --- |
    | Biblioteca di esempio A | +39-0910000001 |
    | Biblioteca di esempio B | (39)0110000002 |
    | Biblioteca di esempio C |  |
    | Biblioteca di esempio D | 0600000004 |

!!! success "Così sì"

    | biblioteca | telefono |
    | --- | --- |
    | Biblioteca di esempio A | +390910000001 |
    | Biblioteca di esempio B | +390110000002 |
    | Biblioteca di esempio C |  |
    | Biblioteca di esempio D | +390600000004 |

## Perché

Con una sola forma, chi riusa i dati può confrontare i numeri, trovare i doppioni e usarli così come sono, anche dall'estero. Con forme diverse deve prima ripulirli uno per uno.

Spazi e trattini creano anche un altro problema: Excel può leggere `+39-0910000001` come una sottrazione, e nella cella resta un numero negativo.

## Casi particolari

- **Più numeri**: una colonna per ogni numero, per esempio `telefono_ufficio` e `telefono_mobile`.
- **Numeri interni**: una colonna a parte, per esempio `interno`. È una colonna di testo, perché può contenere caratteri come `*86` o `#36`.
- **Telefono di un privato**: è un dato personale, vedi [Prima di pubblicare i dati personali](Dati_personali.md).

| biblioteca | telefono | interno |
| --- | --- | --- |
| Biblioteca di esempio A | +390910000001 | *86 |
| Biblioteca di esempio B | +390110000002 | #36 |
| Biblioteca di esempio D | +390600000004 |  |

## Come si fa nel foglio di calcolo

Excel e LibreOffice possono togliere il `+` quando aprono il file: per conservarlo importa la colonna come testo, e non salvare il file dopo averlo aperto con un doppio clic.

- In Excel segui la procedura per [aprire un CSV senza rovinarlo](Linee_guida_importazione_esportazione.md): con il rilevamento automatico dei tipi `+390910000001` diventa un numero, e il `+` si perde.
- In LibreOffice Calc, nella finestra di importazione, imposta come Text la colonna dei telefoni.
- Prima di pubblicare, apri il file con un editor di testo e controlla che il `+` ci sia ancora.

Vedi anche: [5. Se un valore manca, lascia la cella vuota](P05_trattamento_valori_sconosciuti.md), [7. Un solo tipo di dato per colonna](P07_tipi_dati.md), [9. Affianca una descrizione ai codici](P09_campi_codificati.md).
