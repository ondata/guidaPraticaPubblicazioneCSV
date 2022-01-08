# Subtotali, totali o raggruppamenti

Nessuna riga o colonna con totali o subtotali dovrebbe essere inclusa, a meno che non sia assolutamente necessario, mantenendo il massimo livello possibile di disaggregazione dei dati.

Da prendere in considerazione:

- Un file contenente risultati e/o operazioni eseguite sui dati non può essere considerato un file di dati in senso stretto, ma appunto un file contenente i risultati di una determinata analisi dei dati.
- Quando si includono righe o colonne con valori di dati aggregati, per esempio come risultato di un'operazione, è molto difficile e a volte impossibile recuperare i dati disaggregati.
- Un set di dati deve essere coerente al livello di granularità dei dati che contiene. Se il livello di granularità è impostato secondo una certa dimensione, per esempio le vendite mensili, i dati con un altro livello di granularità, per esempio le vendite annuali, non dovrebbero essere mescolati con i precedenti.
- Un livello superiore di granularità può sempre essere ottenuto da un livello inferiore, ma non viceversa. Seguendo l'esempio, è possibile ricavare le vendite annuali dai dati di vendita mensili, ma non è possibile recuperare i dati di vendita mensili dalle vendite annuali.
- Il raggruppamento di righe relative a un'entità, lasciando alcune celle vuote ripetendo l'entità per tutte le righe del raggruppamento dovrebbe essere evitato. Questo problema è comune e può causare problemi quando si cambia l'ordine originale delle righe.

**Esempio 1**: vendite semestrali di automobili (in migliaia), con subtotali (mix di livelli di granularità) e senza subtotali (stesso livello di granularità).

!!! failure "Cattiva prassi"

    | marca | anno | vendite_semestrali |
    | --- | --- | --- |
    | chevrolet chevelle malibu | 1998 | 2.5 |
    | chevrolet chevelle malibu | 1998 | 2.63 |
    | Subtotal anual | 1999 | 5.13 |
    | buick skylark 320 | 1999 | 3.4 |
    | buick skylark 320 | 1999 | 3.57 |
    | Subtotal anual | 1999 | 6.97 |
    | plymouth satellite | 2000 | 2.4 |
    | plymouth satellite | 2000 | 2.52 |
    | Subtotal anual | 2000 | 4.92 |

!!! success "Buona prassi"

    | marca | anno | vendite_s1 | vendite_s2 |
    | --- | --- | --- | --- |
    | chevrolet chevelle malibu | 1998 | 2.5 | 2.63 |
    | buick skylark 320 | 1999 | 3.4 | 3.57 |
    | plymouth satellite | 2000 | 2.4 | 2.52 |

**Esempio 2**: non usare raggruppamenti basati sull'uso di celle vuote.

!!! failure "Cattiva prassi"

    | marca | anno | vendite_semestrali |
    | --- | --- | --- |
    | chevrolet chevelle malibu | 1998 | 2.5 |
    |  | 1999 | 2.63 |
    |  | 2000 | 3.13 |
    | buick skylark 320 | 1998 | 3.4 |
    |  | 1999 | 3.57 |
    |  | 2000 | 3.97 |


!!! success "Buona prassi"

    | marca | anno | vendite_semestrali |
    | --- | --- | --- |
    | chevrolet chevelle malibu | 1998 | 2.5 |
    | chevrolet chevelle malibu | 1999 | 2.63 |
    | chevrolet chevelle malibu | 2000 | 3.13 |
    | buick skylark 320 | 1998 | 3.4 |
    | buick skylark 320 | 1999 | 3.57 |
    | buick skylark 320 | 2000 | 3.97 |

È importante tenere presente che l'esistenza di celle vuote può produrre effetti indesiderati in caso di ordinamento dei dati. La tabella seguente mostra l'effetto dell'ordinamento della tabella iniziale secondo i valori del campo `marca`.

!!! failure "Cattiva prassi"

    | marca | anno | vendite_semestrali |
    | --- | --- | --- |
    | buick skylark 320 | 1998 | 3.4 |
    | chevrolet chevelle malibu | 1998 | 2.5 |
    |  | 1999 | 2.63 |
    |  | 2000 | 3.13 |
    |  | 1999 | 3.57 |
    |  | 2000 | 3.97 |


