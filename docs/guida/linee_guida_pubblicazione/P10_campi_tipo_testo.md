---
hide:
 - toc
# - navigation
title: Metti tra virgolette il testo che lo richiede
---

# 10. Metti tra virgolette il testo che lo richiede

Un testo che contiene una virgola, delle virgolette o un'interruzione di riga deve stare tra virgolette (`"`). Prima di pubblicare devi togliere gli spazi superflui all'inizio e alla fine di un testo.

## Così sì e così no

I nomi delle biblioteche sono inventati. Nel file la riga è scritta così: `Palermo,Biblioteca di esempio A, sede centrale,90133`. La virgola dentro il nome viene letta come separatore, e chi apre il file vede una colonna in più.

!!! failure "Così no"

    | comune | biblioteca | cap |  |
    | --- | --- | --- | --- |
    | Palermo | Biblioteca di esempio A | sede centrale | 90133 |
    | None | Biblioteca di esempio B | 10060 |  |

!!! success "Così sì"

    ```
    comune,biblioteca,cap
    Palermo,"Biblioteca di esempio A, sede centrale",90133
    None,Biblioteca di esempio B,10060
    ```

    | comune | biblioteca | cap |
    | --- | --- | --- |
    | Palermo | Biblioteca di esempio A, sede centrale | 90133 |
    | None | Biblioteca di esempio B | 10060 |

Qui il simbolo `␣` indica uno spazio, che altrimenti non si vedrebbe.

!!! failure "Così no"

    | comune | biblioteca | cap |
    | --- | --- | --- |
    | Palermo | ␣␣Biblioteca di esempio A | 90133 |
    | None | Biblioteca di esempio B␣␣ | 10060 |

!!! success "Così sì"

    | comune | biblioteca | cap |
    | --- | --- | --- |
    | Palermo | Biblioteca di esempio A | 90133 |
    | None | Biblioteca di esempio B | 10060 |

## Perché

Se una virgola nel testo sposta i valori, `sede centrale` finisce nella colonna `cap` e il CAP in una colonna senza nome: tutta la riga è sbagliata, e chi riusa i dati può accorgersene tardi.

Gli spazi sono più difficili da vedere. Secondo la RFC 4180 (il documento che descrive il formato CSV) fanno parte del valore, mentre altri programmi li eliminano: `␣␣Biblioteca di esempio A` e `Biblioteca di esempio A` possono risultare due biblioteche diverse oppure la stessa. Non si può contare sul comportamento di chi legge.

## Casi particolari

- **Virgolette facoltative.** Qualunque testo può stare tra virgolette, anche se non serve: i programmi di lettura le riconoscono e le scartano.
- **Virgolette nel testo.** Si raddoppiano, e l'intero testo deve stare tra virgolette: `Biblioteca "Esempio" B` si scrive `"Biblioteca ""Esempio"" B"`.
- **Interruzioni di riga.** Il testo deve stare tra virgolette, anche se nel file prosegue sulla riga dopo.
- **Spazi che contano.** Se gli spazi all'inizio o alla fine di un testo sono significativi e devono restare, il testo deve stare tra virgolette: `"␣␣Biblioteca di esempio A"`.

Questo file ha insieme virgole, virgolette e un'interruzione di riga, con tre righe di dati e tre colonne in ciascuna:

```
comune,biblioteca,cap
Palermo,"Biblioteca di esempio A, sede centrale",90133
None,"Biblioteca ""Esempio"" B",10060
Roma,"Biblioteca di esempio D
sala ragazzi",00184
```

## Come si fa nel foglio di calcolo

Nelle celle scrivi il testo normalmente, senza virgolette: quando salvi in CSV, Excel e LibreOffice le aggiungono da soli dove servono per il separatore usato, e raddoppiano quelle interne. Per Excel questo significa che, se salva con il `;`, una virgola nel testo resta senza virgolette; la pagina [Esportare un CSV da Excel o LibreOffice](Linee_guida_importazione_esportazione.md) spiega come arrivare alla virgola come separatore.

Per togliere gli spazi superflui in Excel c'è la funzione `ANNULLA.SPAZI` (`TRIM` con i menu in inglese). Riduce a uno anche gli spazi ripetuti dentro il testo.

Vedi anche: [Una riga per ogni record](P02_singolo_record_riga.md), [Scrivi la stessa cosa sempre allo stesso modo](P08_standardizzazione_valori_campi.md), [Dividi gli indirizzi in colonne](P14_campi_tipo_indirizzo_postale.md)
