---
hide:
 - toc
# - navigation
title: Se un valore manca, lascia la cella vuota
---

# 5. Se un valore manca, lascia la cella vuota

Se un valore manca, lascia la cella vuota e spiega nel [dizionario dei dati](../dizionario_dati.md) che cosa significa. Non scrivere mai `0` al posto di un valore mancante.

## Così sì e così no

I nomi delle biblioteche, i telefoni, i prestiti e le spese sono inventati.

!!! failure "Così no"

    | biblioteca | telefono | prestiti | spesa_acquisti_euro |
    | --- | --- | --- | --- |
    | Biblioteca di esempio A | +390910000001 | 12450 | 8200.50 |
    | Biblioteca di esempio B | N/D | 3120 | 1250.00 |
    | Biblioteca di esempio C | - | 0 | 300.00 |
    | Biblioteca di esempio D | NA | 20310 | 15400.75 |

!!! success "Così sì"

    | biblioteca | telefono | prestiti | spesa_acquisti_euro |
    | --- | --- | --- | --- |
    | Biblioteca di esempio A | +390910000001 | 12450 | 8200.50 |
    | Biblioteca di esempio B |  | 3120 | 1250.00 |
    | Biblioteca di esempio C |  |  | 300.00 |
    | Biblioteca di esempio D |  | 20310 | 15400.75 |

Il dizionario dice che cosa significa ogni cella vuota: per `prestiti`, per esempio, «cella vuota = dato non rilevato», come nel [dizionario delle biblioteche](../../risorse/esempi/biblioteche-dizionario.csv).

## Perché

Un `0` al posto di un valore mancante cambia i conti di chi riusa i dati. Nel primo esempio la media dei prestiti è 8970, perché conta lo zero della biblioteca C. Nel secondo è 11960, calcolata sulle tre biblioteche con il dato.

Un testo come `N/D` in una colonna di numeri può far leggere a un programma l'intera colonna come testo. E i valori sconosciuti non spiegati portano spesso a confusione: chi legge non sa se quel dato non esiste, non è stato rilevato o vale zero.

## Casi particolari

!!! note "La posizione europea"

    Le [linee guida europee sulla qualità dei dati](https://op.europa.eu/webpub/op/data-quality-guidelines/en/) considerano ambigua la cella vuota e preferiscono un marcatore esplicito, come `null`. Chi sceglie questa strada usa un solo marcatore in tutto il file e lo dichiara nel dizionario o nello schema (`null` in CSVW, `missingValues` in Table Schema): molti programmi hanno un'opzione per indicare qual è il valore nullo, ma per usarla chi legge deve saperlo.

### Zero non è vuoto

Una cella vuota non significa zero. Se il valore è zero, si scrive `0`.

### Più motivi per la stessa cella vuota

Se la cella vuota può avere più significati (non rilevato, non applicabile, sotto soglia), aggiungi una colonna che spieghi il motivo. Nell'esempio la biblioteca C ha aperto nel 2010, quindi per il 2009 non c'è nulla da contare, mentre per il 2023 il dato non è stato rilevato. La biblioteca B nel 2022 ha fatto zero prestiti.

| biblioteca | anno | prestiti | motivo_prestiti_mancanti |
| --- | --- | --- | --- |
| Biblioteca di esempio B | 2022 | 0 |  |
| Biblioteca di esempio B | 2023 | 3120 |  |
| Biblioteca di esempio C | 2009 |  | non applicabile |
| Biblioteca di esempio C | 2023 |  | non rilevato |

Lo stesso accade quando uno strumento registra solo i valori sopra una certa soglia, come un sensore di inquinamento: il motivo va nella colonna aggiunta e nel dizionario dei dati.

### Evita `NA`

`NA` è anche la sigla di Napoli: alcuni programmi lo leggono come valore mancante anche quando è un dato. Con pandas 3.1, una libreria di Python per l'analisi dei dati, lo stesso succede al nome del comune di `None`, in provincia di Torino: con le opzioni predefinite entrambi diventano valori mancanti.

Vedi anche: [4. Righe nuove, non colonne nuove](P04_strutture_dati_verticale_orizzontale.md), [7. Un solo tipo di dato per colonna](P07_tipi_dati.md), [8. Scrivi la stessa cosa sempre allo stesso modo](P08_standardizzazione_valori_campi.md).
