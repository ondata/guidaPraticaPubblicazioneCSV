---
hide:
 - toc
# - navigation
title: Niente totali e subtotali
---

# 6. Niente totali e subtotali

Il file deve contenere solo righe di dettaglio, tutte allo stesso livello, senza righe o colonne di totali e subtotali. Ogni riga deve riportare tutti i suoi valori, senza celle lasciate vuote per raggruppare le righe.

## Così sì e così no

Nomi delle biblioteche e numeri sono inventati, i codici Istat e i nomi dei comuni sono veri. Il primo esempio mostra una riga di totale.

!!! failure "Così no"

    | comune | biblioteca | anno | spesa_acquisti_euro |
    | --- | --- | --- | ---: |
    | Palermo | Biblioteca di esempio A | 2023 | 8200.50 |
    | None | Biblioteca di esempio B | 2023 | 1250.00 |
    | Cella Dati | Biblioteca di esempio C | 2023 | 300.00 |
    | Roma | Biblioteca di esempio D | 2023 | 15400.75 |
    | Totale |  | 2023 | 25151.25 |

!!! success "Così sì"

    | comune | biblioteca | anno | spesa_acquisti_euro |
    | --- | --- | --- | ---: |
    | Palermo | Biblioteca di esempio A | 2023 | 8200.50 |
    | None | Biblioteca di esempio B | 2023 | 1250.00 |
    | Cella Dati | Biblioteca di esempio C | 2023 | 300.00 |
    | Roma | Biblioteca di esempio D | 2023 | 15400.75 |

Il secondo esempio mescola due livelli di dettaglio: i prestiti di ogni semestre e il loro subtotale annuale.

!!! failure "Così no"

    | biblioteca | anno | semestre | prestiti |
    | --- | ---: | ---: | ---: |
    | Biblioteca di esempio A | 2023 | 1 | 6100 |
    | Biblioteca di esempio A | 2023 | 2 | 6350 |
    | Subtotale annuale | 2023 |  | 12450 |
    | Biblioteca di esempio D | 2023 | 1 | 9800 |
    | Biblioteca di esempio D | 2023 | 2 | 10510 |
    | Subtotale annuale | 2023 |  | 20310 |

!!! success "Così sì"

    | biblioteca | anno | semestre | prestiti |
    | --- | ---: | ---: | ---: |
    | Biblioteca di esempio A | 2023 | 1 | 6100 |
    | Biblioteca di esempio A | 2023 | 2 | 6350 |
    | Biblioteca di esempio D | 2023 | 1 | 9800 |
    | Biblioteca di esempio D | 2023 | 2 | 10510 |

Il terzo esempio usa le celle vuote per raggruppare: il comune e la biblioteca sono scritti solo nella prima riga del gruppo.

!!! failure "Così no"

    | comune | biblioteca | semestre | prestiti |
    | --- | --- | ---: | ---: |
    | Palermo | Biblioteca di esempio A | 1 | 6100 |
    |  |  | 2 | 6350 |
    | Roma | Biblioteca di esempio D | 1 | 9800 |
    |  |  | 2 | 10510 |

!!! success "Così sì"

    | comune | biblioteca | semestre | prestiti |
    | --- | --- | ---: | ---: |
    | Palermo | Biblioteca di esempio A | 1 | 6100 |
    | Palermo | Biblioteca di esempio A | 2 | 6350 |
    | Roma | Biblioteca di esempio D | 1 | 9800 |
    | Roma | Biblioteca di esempio D | 2 | 10510 |

Le celle vuote reggono solo finché nessuno cambia l'ordine delle righe. Ecco la tabella con le celle vuote dopo un ordinamento per `comune`: le righe del secondo semestre finiscono in fondo e non si capisce più a quale biblioteca appartengono.

!!! failure "Così no"

    | comune | biblioteca | semestre | prestiti |
    | --- | --- | ---: | ---: |
    | Palermo | Biblioteca di esempio A | 1 | 6100 |
    | Roma | Biblioteca di esempio D | 1 | 9800 |
    |  |  | 2 | 6350 |
    |  |  | 2 | 10510 |

## Perché

Chi riusa i dati fa i conti sulla colonna. Con la riga `Totale` la somma di `spesa_acquisti_euro` dà 50302.50 invece di 25151.25, perché ogni importo viene contato due volte, e prima di ogni calcolo bisogna scoprire quali righe togliere.

Il dettaglio è la scelta che lascia aperte tutte le strade. Dai prestiti di ogni semestre si ricavano quelli dell'anno, ma dal totale dell'anno non si risale ai semestri. Un file che contiene risultati od operazioni fatte sui dati è il risultato di un'analisi, non un file di dati in senso stretto.

## Casi particolari

- **Livello di dettaglio.** Un dataset deve restare a un solo livello, detto anche granularità: se le righe sono mensili, non devono esserci anche righe annuali. Pubblica il livello più dettagliato che hai.
- **Colonne di totale.** La regola vale anche per le colonne: niente `prestiti_totale` accanto ai prestiti di ogni semestre.
- **Totali utili a chi legge.** Se servono, offrili in un file a parte, accanto a quello di dettaglio.

Vedi anche: [Una riga per ogni record](P02_singolo_record_riga.md), [Righe nuove, non colonne nuove](P04_strutture_dati_verticale_orizzontale.md), [Se un valore manca, lascia la cella vuota](P05_trattamento_valori_sconosciuti.md)
