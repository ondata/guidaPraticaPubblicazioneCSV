---
hide:
 - toc
# - navigation
title: Una sola riga di intestazione
---

# 1. Una sola riga di intestazione

Il file contiene sempre una, e una sola, riga di intestazione, nella prima riga. Il formato CSV ammette anche file senza intestazione (RFC 4180), ma chi pubblica dati non dovrebbe usare questa possibilità: lo raccomandano anche le [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/allegato-B.html#csv).

## Così sì e così no

I nomi delle biblioteche e le spese sono inventati.

Non mettere titoli o note sopra l'intestazione.

!!! failure "Così no"

    | Biblioteche comunali |  |  |  |
    | --- | --- | --- | --- |
    | Dati del 2023 |  |  |  |
    | comune | biblioteca | anno | spesa_acquisti_euro |
    | Palermo | Biblioteca di esempio A | 2023 | 8200.50 |
    | Roma | Biblioteca di esempio D | 2023 | 15400.75 |

!!! success "Così sì"

    | comune | biblioteca | anno | spesa_acquisti_euro |
    | --- | --- | --- | --- |
    | Palermo | Biblioteca di esempio A | 2023 | 8200.50 |
    | Roma | Biblioteca di esempio D | 2023 | 15400.75 |

Le informazioni delle righe tolte vanno nel [dizionario dei dati](../dizionario_dati.md) o nella descrizione del dataset. L'anno, se serve, sta in una colonna.

Non unire le celle dell'intestazione: ogni colonna ha una sola cella con il suo nome. Qui `indirizzo` è una cella unita sulle ultime tre colonne, e i nomi veri stanno nella riga sotto.

!!! failure "Così no"

    | biblioteca | indirizzo |  |  |
    | --- | --- | --- | --- |
    |  | dug | denominazione | civico |
    | Biblioteca di esempio A | Via | Roma | 10 |
    | Biblioteca di esempio D | Via | Cavour | 20 |

!!! success "Così sì"

    | biblioteca | dug | denominazione | civico |
    | --- | --- | --- | --- |
    | Biblioteca di esempio A | Via | Roma | 10 |
    | Biblioteca di esempio D | Via | Cavour | 20 |

## Perché

Un programma prende la prima riga come nomi di colonna e tutte le altre come dati. Con le due righe di titolo, `Biblioteche comunali` diventa il nome della prima colonna, le altre restano senza nome e la vera intestazione finisce fra i dati. Anche `spesa_acquisti_euro` diventa testo, perché contiene quella parola in mezzo ai numeri, e chi riusa il file deve ripulirlo a mano prima di fare una somma.

Più righe di intestazione aiutano l'occhio di chi legge e ostacolano i programmi. Il CSV non conosce le celle unite: una cella unita lascia celle vuote accanto al nome, e per sapere come si chiama una colonna occorre leggere due righe.

I nomi di colonna descrivono i dati ma non ne fanno parte: un file con l'intestazione e quattro biblioteche ha quattro righe di dati.

## Casi particolari

### File ereditati senza intestazione

Meglio aggiungere l'intestazione. Se non puoi, devi dichiarare che manca: nessun programma può capirlo da solo, perché la prima riga è scritta come tutte le altre.

!!! note "Come dichiararlo"

    In CSVW con `"dialect": {"header": false}`, in Table Dialect con `"header": false`, oppure via HTTP con `Content-Type: text/csv;header=absent`. Chi pubblica uno schema CSVW può mettere nella proprietà `dc:description` anche le informazioni tolte dalle righe di titolo.

## Come si fa nel foglio di calcolo

Prima di esportare il CSV:

1. Elimina le righe sopra l'intestazione, così che i nomi di colonna stiano nella riga 1.
2. Annulla l'unione delle celle e scrivi un nome in ogni colonna.
3. Sposta titoli, legende e note in un altro foglio o nel dizionario dei dati.

Per l'esportazione vedi [Esportare un CSV da Excel o LibreOffice](Linee_guida_importazione_esportazione.md).

Vedi anche: [2. Una riga per ogni record](P02_singolo_record_riga.md), [3. Nomi di colonna chiari](P03_denominazione_colonne.md), [6. Niente totali e subtotali](P06_subtotali_totali_raggruppamenti.md).
