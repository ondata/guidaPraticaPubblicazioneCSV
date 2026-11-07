---
hide:
- toc
# - navigation
title: Scrivi le date come AAAA-MM-GG
---

# 12. Scrivi le date come AAAA-MM-GG

Le date devono seguire la norma [ISO 8601](https://it.wikipedia.org/wiki/ISO_8601): `AAAA-MM-GG` per le date, come `1985-03-12`, e `AAAA-MM-GGTHH:MM:SS` per data e ora insieme.

## Così sì e così no

Nomi delle biblioteche, date e orari di questa pagina sono inventati.

!!! failure "Così no"

    | biblioteca | data_apertura |
    | --- | --- |
    | Biblioteca di esempio A | 12 marzo 1985 |
    | Biblioteca di esempio B | 30/09/2001 |
    | Biblioteca di esempio C | 15-01-10 |
    | Biblioteca di esempio D | 1 giugno 1998 |

!!! success "Così sì"

    | biblioteca | data_apertura |
    | --- | --- |
    | Biblioteca di esempio A | 1985-03-12 |
    | Biblioteca di esempio B | 2001-09-30 |
    | Biblioteca di esempio C | 2010-01-15 |
    | Biblioteca di esempio D | 1998-06-01 |

## Perché

`03/04/2023` è il 3 aprile per chi legge in Italia e il 4 marzo per chi legge negli Stati Uniti, e `15-01-10` non dice nemmeno quale numero sia l'anno. `AAAA-MM-GG` ha un solo significato e si ordina da solo: anche ordinate come testo, le date risultano in ordine cronologico.

## Casi particolari

### Come si scrive

- **Zeri**: mese, giorno, ore, minuti e secondi hanno sempre due cifre: `03`, non `3`.
- **Separatori**: `-` nelle date, `:` nelle ore, la lettera `T` tra data e ora.

### Date incomplete

Usa la data completa, `AAAA-MM-GG`, quando la conosci. Se il dato è mensile usa `AAAA-MM`, mai `AAAAMM`; se è annuale, `AAAA`.

Non inventare il giorno che manca: l'ultimo giorno del mese si usa solo quando il dato si riferisce davvero a quel giorno, per esempio una consistenza al 31 dicembre. Le colonne `anno` e `mese` separate restano un'alternativa.

| biblioteca | mese | prestiti |
| --- | --- | ---: |
| Biblioteca di esempio A | 2023-07 | 1040 |
| Biblioteca di esempio A | 2023-08 | 615 |

### Ore

Meglio il formato 24 ore, `HH:MM:SS`, rispetto al formato 12 ore con AM e PM. Data e ora stanno in una sola colonna, nel formato `AAAA-MM-GGTHH:MM:SS`.

Indica lo scostamento dal tempo coordinato universale (UTC): `2026-07-23T16:34:00+02:00`, oppure `2026-07-23T14:34:00Z`. Sono lo stesso istante: `+02:00` dice che l'orologio locale è due ore avanti rispetto a UTC, `Z` che l'orario è già in UTC. In Italia lo scostamento è `+01:00` in inverno e `+02:00` in estate. Se tutti gli orari sono locali e non puoi indicare lo scostamento, dichiaralo nel [dizionario dei dati](../dizionario_dati.md).

!!! failure "Così no"

    | biblioteca | ultimo_prestito |
    | --- | --- |
    | Biblioteca di esempio A | 29 dicembre 2023, alle 15:10 |
    | Biblioteca di esempio B | 14/07/2023 - 04:34 PM |
    | Biblioteca di esempio D | 1-Febbraio-2023-12-23-34 |

!!! success "Così sì"

    | biblioteca | ultimo_prestito |
    | --- | --- |
    | Biblioteca di esempio A | 2023-12-29T15:10:00+01:00 |
    | Biblioteca di esempio B | 2023-07-14T16:34:00+02:00 |
    | Biblioteca di esempio D | 2023-02-01T12:23:34+01:00 |

## Come si fa nel foglio di calcolo

- Prima di esportare, usa per le date il formato `aaaa-mm-gg`: le celle escono come sono visualizzate, e una data può uscire come `31/01/2023`.
- Excel può trasformare `2023-07` in una data, `01/07/2023`, quando apre il file. Per evitarlo segui la procedura per [aprire un CSV in Excel](Linee_guida_importazione_esportazione.md#aprire-un-csv-in-excel-senza-rovinarlo). In LibreOffice Calc, nella finestra di importazione, imposta come Testo (Text) le colonne con i mesi.
- Prima di pubblicare, apri il file con un editor di testo e controlla che le date siano scritte come `1985-03-12`.

Vedi anche: [4. Righe nuove, non colonne nuove](P04_strutture_dati_verticale_orizzontale.md), [7. Un solo tipo di dato per colonna](P07_tipi_dati.md), [8. Scrivi la stessa cosa sempre allo stesso modo](P08_standardizzazione_valori_campi.md).
