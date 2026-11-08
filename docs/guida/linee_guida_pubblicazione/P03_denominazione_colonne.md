---
hide:
 - toc
# - navigation
title: Nomi di colonna chiari
---

# 3. Nomi di colonna chiari

I nomi di colonna devono essere comprensibili alle persone, e meglio se scritti in modo che i programmi li leggano senza intoppi: minuscole, cifre e trattini bassi.

## Così sì e così no

I nomi delle biblioteche, i telefoni, i prestiti e le spese sono inventati.

!!! failure "Così no"

    | Cod. Istat | Comune | Nome | Tel. | N. prestiti | Spesa (€) |
    | --- | --- | --- | --- | --- | --- |
    | 082053 | Palermo | Biblioteca di esempio A | +390910000001 | 12450 | 8200.50 |
    | 058091 | Roma | Biblioteca di esempio D | +390600000004 | 20310 | 15400.75 |

!!! success "Così sì"

    | codice_istat_comune | comune | biblioteca | telefono | prestiti | spesa_acquisti_euro |
    | --- | --- | --- | --- | --- | --- |
    | 082053 | Palermo | Biblioteca di esempio A | +390910000001 | 12450 | 8200.50 |
    | 058091 | Roma | Biblioteca di esempio D | +390600000004 | 20310 | 15400.75 |

I nomi di colonna:

- **Unici.** Due colonne non devono avere lo stesso nome.
- **Allineati al dizionario.** Devono coincidere con quelli del [dizionario dei dati](../dizionario_dati.md).
- **Brevi.** Meglio corti, purché il risparmio di caratteri non porti a capire male.
- **Senza abbreviazioni e codici.** Meglio evitarli. Se un codice serve davvero, va spiegato nel dizionario dei dati.
- **Senza una cifra iniziale.** Meglio che comincino con una lettera.
- **Solo minuscole e cifre.** Meglio usare solo le lettere a-z e le cifre 0-9, senza accenti (`à`, `è`, `ü`), punteggiatura o simboli.
- **Trattini bassi al posto degli spazi.** Meglio separare le parole con `_`.

Se l'unità di misura è la stessa per tutta la colonna, si indica nel nome, come in `spesa_acquisti_euro`: vedi la [scheda 7](P07_tipi_dati.md).

## Perché

Chi riusa i dati scrive questi nomi nelle formule e nei programmi. Spazi, punti e simboli come `(€)` spesso costringono a metterli tra virgolette, e un accento si può storpiare se il file viene letto con un'altra codifica. Chi legge `Nome` non sa di cosa è il nome: deve andare a chiedere o tirare a indovinare.

## Casi particolari

### Nomi che arrivano dal gestionale

Spesso le colonne conservano i nomi assegnati dal sistema che gestisce i dati, scritti secondo convenzioni tecniche difficili da capire. Meglio rinominarle prima di pubblicare.

### Più colonne sulla stessa cosa

Se più colonne descrivono la stessa cosa, meglio far iniziare il nome con quella cosa e proseguire con il dettaglio, dal generale al particolare. Così le colonne si ritrovano vicine in ordine alfabetico e si capisce a chi si riferisce ciascuna.

| biblioteca_nome | biblioteca_telefono | ente_nome | ente_telefono |
| --- | --- | --- | --- |
| Biblioteca di esempio A | +390910000001 | Comune di Palermo | +390910000099 |

### Identificatori e descrizioni

Una colonna che contiene un identificatore può avere il suffisso `_id`. Fa eccezione il caso in cui un altro nome dice di più, perché indica il sistema di identificazione usato, come `codice_ipa` o `codice_istat_comune`.

Per la colonna con la descrizione di quell'identificatore è consigliato il suffisso `_nome`, a meno che un altro nome sia più chiaro.

| biblioteca_id | biblioteca_nome |
| --- | --- |
| BIB001 | Biblioteca di esempio A |

Vedi anche: [1. Una sola riga di intestazione](P01_unica_riga_intestazione.md), [7. Un solo tipo di dato per colonna](P07_tipi_dati.md), [9. Affianca una descrizione ai codici](P09_campi_codificati.md).
