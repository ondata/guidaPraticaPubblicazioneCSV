# Trattamento dei valori sconosciuti

- I valori dei dati devono essere completi ed espressi in un modo che sia accurato e coerente con il tipo di dati del campo, in modo che possano essere trattati nei termini del loro valore effettivo.

- Come regola generale, tutte le celle di una tabella dovrebbero essere valorizzate e dovrebbe essere scelto un codice comune per i dati sconosciuti.

- Da prendere in considerazione:
    - I valori sconosciuti, quando non vengono spiegati o sono semplicemente assenti, portano spesso a confusione, specialmente quando la colonna di dati è numerica. D'altra parte, generano risultati errati in termini di ordinamento.
    - Raccomandazioni per evitare valori di dati sconosciuti:
         - Se la cella vuota rappresenta uno zero, allora il valore deve essere `0`.
         - Se la cella vuota rappresenta un valore "sconosciuto" o "non ottenuto", allora questa possibilità deve essere spiegata nel dizionario dei dati e indicata con un codice specifico.
         - Se un valore vuoto ha un significato, dovrebbe essere considerata l'opzione di aggiungere una nuova colonna, per includere la spiegazione del valore "vuoto" come possibile valore.
         - Una terminologia accettata per indicare valori sconosciuti o mancanti è il valore/codice NA o N/A[^1].
         - Il codice usato per indicare valori sconosciuti o mancanti, ad esempio NA, deve essere specificato nel dizionario dei dati.

## Esempio 1

!!! failure "Cattiva prassi"

    | marca | anno | consumo | vendite |
    | --- | --- | --- | ---: |
    | chevrolet chevelle malibu | 1998 | Alto | 2.5 |
    | chevrolet chevelle malibu | 1999 | Bajo | 2.63 |
    | chevrolet chevelle malibu | 2000 | Medio |  |
    | buick skylark 320 | 1998 |  | 3.4 |
    | buick skylark 320 | 1999 | Medio | 3.57 |
    | buick skylark 320 | 2000 | Medio | N/A |
    | plymouth satellite | 1998 |  | 2.4 |
    | plymouth satellite | 1999 |  | 2.52 |
    | plymouth satellite | 2000 | Alto | 3.6 |

!!! success "Buona prassi"

    | marca | anno | consumo | vendite |
    | --- | --- | --- | ---: |
    | chevrolet chevelle malibu | 1998 | Alto | 2.5 |
    | chevrolet chevelle malibu | 1999 | Bajo | 2.63 |
    | chevrolet chevelle malibu | 2000 | Medio | 0 |
    | buick skylark 320 | 1998 | NA | 3.4 |
    | buick skylark 320 | 1999 | Medio | 3.57 |
    | buick skylark 320 | 2000 | Medio | NA |
    | plymouth satellite | 1998 | NA | 2.4 |
    | plymouth satellite | 1999 | NA | 2.52 |
    | plymouth satellite | 2000 | Alto | 3.6 |

Nell'esempio si osserva che il valore `0` nella colonna "vendite", indica che per quell'anno le vendite di auto di quel modello sono state `0`. Quando invece il dato di "vendite" e/o di "consumo" è sconosciuto, è indicato con `NA`. Tutti i valori sconosciuti in qualsiasi colonna sono indicati con lo stesso codice: `NA`.

## Esempio 2

!!! success "Cattiva prassi"

    | marca | anno | consumo | vendite |
    | --- | --- | --- | ---: |
    | chevrolet chevelle malibu | 1998 | Alto | 2.5 |
    | chevrolet chevelle malibu | 1999 | Bajo | 2.63 |
    | chevrolet chevelle malibu | 2000 | Medio |  |
    | buick skylark 320 | 1998 | NA | 3.4 |
    | buick skylark 320 | 1999 | Medio | 3.57 |
    | buick skylark 320 | 2000 | Medio |  |
    | plymouth satellite | 1998 | NA | 2.4 |
    | plymouth satellite | 1999 | NA | 2.52 |
    | plymouth satellite | 2000 | Alto | 3.6 |

!!! success "Buona prassi"

    | marca | anno | consumo | vendite | Significato valore mancante vendite |
    | --- | --- | --- | ---: | --- |
    | chevrolet chevelle malibu | 1998 | Alto | 2.5 |  |
    | chevrolet chevelle malibu | 1999 | Bajo | 2.63 |  |
    | chevrolet chevelle malibu | 2000 | Medio |  |  |
    | buick skylark 320 | 1998 | NA | 3.4 | <soglia minima (0.1) |
    | buick skylark 320 | 1999 | Medio | 3.57 |  |
    | buick skylark 320 | 2000 | Medio |  |  |
    | plymouth satellite | 1998 | NA | 2.4 | <soglia minima (0.1) |
    | plymouth satellite | 1999 | NA | 2.52 |  |
    | plymouth satellite | 2000 | Alto | 3.6 |  |


Nell'esempio viene aggiunta una nuova colonna per spiegare il significato del valore mancante nella colonna “vendite”.
Ci sono circostanze in cui determinate misurazioni non possono essere registrate, perché i dispositivi o i sistemi utilizzati per misurare determinate grandezze registrano solo valori al di sopra di una certa soglia (ad esempio un sensore di inquinamento ambientale). In questi casi, sarà spiegato nel dizionario dei dati e indicato nella tabella con un codice comune.



[^1]: Dall'inglese, *not available* (non disponibile), *not applicable* (non applicabile al caso) o *no answer* (nessuna risposta; sebbene questo significato viene utilizzato solo in determinate situazioni). <https://es.wikipedia.org/wiki/N/a>

