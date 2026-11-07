---
hide:
 - toc
# - navigation
title: Righe nuove, non colonne nuove
---

# 4. Righe nuove, non colonne nuove

Quando i dati crescono, per un anno o una categoria in più, devi aggiungere righe e non colonne: una colonna per ogni tipo di informazione, una riga per ogni dato, per esempio i prestiti di una biblioteca in un anno.

## Così sì e così no

I nomi delle biblioteche e i prestiti sono inventati.

Una serie temporale cresce per righe, non per colonne: `anno` è una colonna. La forma con una colonna per anno, detta larga, si può offrire come file aggiuntivo di consultazione, accanto a quella con una riga per anno, detta lunga.

!!! failure "Così no"

    | biblioteca | 2021 | 2022 | 2023 |
    | --- | --- | --- | --- |
    | Biblioteca di esempio A | 11800 | 12100 | 12450 |
    | Biblioteca di esempio D | 19750 | 20040 | 20310 |

!!! success "Così sì"

    | biblioteca | anno | prestiti |
    | --- | --- | --- |
    | Biblioteca di esempio A | 2021 | 11800 |
    | Biblioteca di esempio A | 2022 | 12100 |
    | Biblioteca di esempio A | 2023 | 12450 |
    | Biblioteca di esempio D | 2021 | 19750 |
    | Biblioteca di esempio D | 2022 | 20040 |
    | Biblioteca di esempio D | 2023 | 20310 |

Vale anche per le categorie. Una colonna per ogni tipo di prestito obbliga a cambiare la struttura del file ogni volta che ne compare uno nuovo.

!!! failure "Così no"

    | biblioteca | anno | prestiti_libri | prestiti_dvd | prestiti_periodici |
    | --- | --- | --- | --- | --- |
    | Biblioteca di esempio A | 2023 | 11000 | 1200 | 250 |
    | Biblioteca di esempio D | 2023 | 18000 | 1800 | 510 |

!!! success "Così sì"

    | biblioteca | anno | tipo_prestito | prestiti |
    | --- | --- | --- | --- |
    | Biblioteca di esempio A | 2023 | libri | 11000 |
    | Biblioteca di esempio A | 2023 | dvd | 1200 |
    | Biblioteca di esempio A | 2023 | periodici | 250 |
    | Biblioteca di esempio D | 2023 | libri | 18000 |
    | Biblioteca di esempio D | 2023 | dvd | 1800 |
    | Biblioteca di esempio D | 2023 | periodici | 510 |

## Perché

Immagina un registro: ogni anno aggiungi una riga in fondo alla pagina, non ristampi il modulo con una colonna in più. Con una colonna per anno, ogni aggiornamento cambia la struttura del file, e chi ha costruito un foglio, un grafico o un programma su quel file deve correggerli.

Nella forma lunga si filtra un anno, si ordina per prestiti e si confrontano i gruppi con le funzioni di base di qualsiasi programma. Nella forma larga anche un grafico dell'andamento richiede di ricostruire prima la colonna `anno`.

## Casi particolari

### Quando una colonna nuova serve davvero

Una colonna nuova serve quando arriva un'informazione mai raccolta prima, non un altro valore di una che già c'è. Nelle righe precedenti, dove quel valore non esiste, la cella resta vuota.

| biblioteca | anno | prestiti | spesa_acquisti_euro |
| --- | --- | --- | --- |
| Biblioteca di esempio A | 2022 | 12100 |  |
| Biblioteca di esempio A | 2023 | 12450 | 8200.50 |

Vedi anche: [2. Una riga per ogni record](P02_singolo_record_riga.md), [5. Se un valore manca, lascia la cella vuota](P05_trattamento_valori_sconosciuti.md), [6. Niente totali e subtotali](P06_subtotali_totali_raggruppamenti.md).
