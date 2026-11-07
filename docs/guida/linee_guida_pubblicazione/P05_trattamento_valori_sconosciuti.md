---
hide:
 - toc
# - navigation
title: Trattamento dei valori sconosciuti o nulli
---

# Trattamento dei valori sconosciuti o nulli

- I valori dei dati devono essere completi ed espressi in un modo che sia accurato e coerente con il tipo di dati del campo, in modo che possano essere trattati nei termini del loro valore effettivo.

- Se un valore manca, lascia la cella vuota e spiega nel [dizionario dei dati](../dizionario_dati.md) che cosa significa.

- Da prendere in considerazione:
    - I valori sconosciuti, quando non vengono spiegati, portano spesso a confusione, specialmente quando la colonna di dati è numerica.
    - Raccomandazioni:
         - Una cella vuota non significa zero: se il valore è zero, si scrive `0`.
         - Se la cella vuota può avere più significati (non rilevato, non applicabile, sotto soglia), aggiungi una colonna che spieghi il motivo.
         - Evita `NA`, che è anche la sigla di Napoli: alcuni programmi lo leggono come valore mancante anche quando è un dato.

!!! note "La posizione europea"

    Le [linee guida europee sulla qualità dei dati](https://op.europa.eu/webpub/op/data-quality-guidelines/en/) considerano ambigua la cella vuota e preferiscono un marcatore esplicito, come `null`. Chi sceglie questa strada usa un solo marcatore in tutto il file e lo dichiara nel dizionario o nello schema (`null` in CSVW, `missingValues` in Table Schema): molti programmi hanno un'opzione per indicare qual è il valore nullo, ma per usarla chi legge deve saperlo.

### Esempio 1

!!! failure "Cattiva prassi"

    | marca | anno | consumo | vendite |
    | --- | --- | --- | ---: |
    | chevrolet chevelle malibu | 1998 | Alto | 2.5 |
    | chevrolet chevelle malibu | 1999 | Basso | 2.63 |
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
    | chevrolet chevelle malibu | 1999 | Basso | 2.63 |
    | chevrolet chevelle malibu | 2000 | Medio | 0 |
    | buick skylark 320 | 1998 |  | 3.4 |
    | buick skylark 320 | 1999 | Medio | 3.57 |
    | buick skylark 320 | 2000 | Medio |  |
    | plymouth satellite | 1998 |  | 2.4 |
    | plymouth satellite | 1999 |  | 2.52 |
    | plymouth satellite | 2000 | Alto | 3.6 |

Nell'esempio si osserva che il valore `0` nella colonna "vendite" indica che per quell'anno le vendite di auto di quel modello sono state `0`. Quando invece il dato di "vendite" e/o di "consumo" è sconosciuto, la cella è vuota, in tutte le colonne.

### Esempio 2

!!! failure "Cattiva prassi"

    | marca | anno | consumo | vendite |
    | --- | --- | --- | ---: |
    | chevrolet chevelle malibu | 1998 | Alto | 2.5 |
    | chevrolet chevelle malibu | 1999 | Basso | 2.63 |
    | chevrolet chevelle malibu | 2000 | Medio |  |
    | buick skylark 320 | 1998 |  | 3.4 |
    | buick skylark 320 | 1999 | Medio | 3.57 |
    | buick skylark 320 | 2000 | Medio |  |
    | plymouth satellite | 1998 |  | 2.4 |
    | plymouth satellite | 1999 |  | 2.52 |
    | plymouth satellite | 2000 | Alto | 3.6 |

!!! success "Buona prassi"

    | marca | anno | consumo | vendite | significato_valore_mancante_vendite |
    | --- | --- | --- | --- | --- |
    | chevrolet chevelle malibu | 1998 | Alto | 2.5 |  |
    | chevrolet chevelle malibu | 1999 | Basso | 2.63 |  |
    | chevrolet chevelle malibu | 2000 | Medio |  | <soglia minima (0.1) |
    | buick skylark 320 | 1998 |  | 3.4 |  |
    | buick skylark 320 | 1999 | Medio | 3.57 |  |
    | buick skylark 320 | 2000 | Medio |  | <soglia minima (0.1) |
    | plymouth satellite | 1998 |  | 2.4 |  |
    | plymouth satellite | 1999 |  | 2.52 |  |
    | plymouth satellite | 2000 | Alto | 3.6 |  |


Nell'esempio viene aggiunta una nuova colonna per spiegare il significato del valore mancante nella colonna “vendite”.
Ci sono circostanze in cui determinate misurazioni non possono essere registrate, perché i dispositivi o i sistemi utilizzati per misurare determinate grandezze registrano solo valori al di sopra di una certa soglia (ad esempio un sensore di inquinamento ambientale). In questi casi, il motivo si spiega nel dizionario dei dati e nella colonna aggiunta.
