---
hide:
 - toc
# - navigation
title: Scrivi la stessa cosa sempre allo stesso modo
---

# 8. Scrivi la stessa cosa sempre allo stesso modo

Un valore deve essere scritto sempre allo stesso modo in tutta la tabella: se scegli `Palermo`, non usi anche `Comune di Palermo`. Quando esiste un codice o un vocabolario standard, è consigliato usarlo.

## Così sì e così no

Nomi delle biblioteche e prestiti sono inventati, i codici Istat e i nomi dei comuni sono veri. Qui lo stesso comune è scritto in due modi.

!!! failure "Così no"

    | comune | biblioteca | anno | prestiti |
    | --- | --- | ---: | ---: |
    | Palermo | Biblioteca di esempio A | 2022 | 12100 |
    | Comune di Palermo | Biblioteca di esempio A | 2023 | 12450 |
    | Roma | Biblioteca di esempio D | 2022 | 20040 |
    | ROMA | Biblioteca di esempio D | 2023 | 20310 |

!!! success "Così sì"

    | codice_istat_comune | comune | biblioteca | anno | prestiti |
    | --- | --- | --- | ---: | ---: |
    | 082053 | Palermo | Biblioteca di esempio A | 2022 | 12100 |
    | 082053 | Palermo | Biblioteca di esempio A | 2023 | 12450 |
    | 058091 | Roma | Biblioteca di esempio D | 2022 | 20040 |
    | 058091 | Roma | Biblioteca di esempio D | 2023 | 20310 |

## Perché

Per un programma `Palermo` e `Comune di Palermo` sono due comuni diversi. Chi filtra le righe di Palermo perde quelle scritte nell'altro modo, e chi conta i prestiti per comune ottiene quattro comuni invece di due.

Un codice standard è come una chiave uguale per tutte le porte: chi ha un altro dataset con il codice Istat del comune può unirlo al tuo senza confrontare i nomi. Con i soli nomi è facile sbagliare: si trova `Reggio Emilia` al posto di `Reggio nell'Emilia` (`035033`) e `Reggio Calabria` al posto di `Reggio di Calabria` (`080063`).

## Casi particolari

- **Tra un dataset e l'altro.** È consigliato usare la stessa codifica e la stessa struttura per lo stesso tipo di dato in tutti i dataset di un catalogo: per esempio gli indirizzi hanno sempre le stesse colonne e i dati geografici lo stesso sistema di coordinate.
- **Standard comuni.** Meglio usare gli standard che altri già usano, come le classificazioni di [Eurostat](https://ec.europa.eu/eurostat/web/nace) e di [Istat](https://www.istat.it/it/metodi-e-strumenti/classificazioni), e vocabolari di uso comune[^1]. Prima di inventare un elenco di valori, guarda se esiste già tra i [vocabolari nazionali](Tassonomie_elenchi_codici.md#vocabolari-nazionali).
- **Senza un vocabolario di riferimento.** Il valore scelto deve comunque essere unico e coerente in tutta la tabella.
- **Attività economica.** Il riferimento è la [classificazione Ateco 2025 di Istat](https://www.istat.it/classificazione/ateco-2025/), dove `91.11` è «Attività di biblioteche». Le classificazioni hanno versioni: dichiara quella usata, per esempio nel nome della colonna (`codice_ateco_2025`).
- **Codici che cambiano.** I codici Istat cambiano con fusioni e riforme territoriali: indica nel dizionario dei dati la data dei codici usati. Vedi [Codici e classificazioni](Tassonomie_elenchi_codici.md).
- **Tempo di riferimento.** Ogni dato si riferisce a un momento. I prestiti sono un dato annuale, quindi serve una colonna che indichi l'anno, come `anno` nell'esempio.

[^1]: Le [Linee guida dell'Agenzia per l'Italia digitale (AgID)](https://ondata.github.io/linee-guida-opendata/capitolo-5.html#sec-arricchimento) indicano il Catalogo nazionale della semantica dei dati.

Vedi anche: [9. Affianca una descrizione ai codici](P09_campi_codificati.md), [14. Dividi gli indirizzi in colonne](P14_campi_tipo_indirizzo_postale.md), [Codici e classificazioni](Tassonomie_elenchi_codici.md).
