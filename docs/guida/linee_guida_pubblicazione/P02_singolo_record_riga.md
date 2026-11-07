---
hide:
 - toc
# - navigation
title: Una riga per ogni record
---

# 2. Una riga per ogni record

Ogni riga del file, detta anche record, deve descrivere una sola cosa, e ogni cosa descritta deve stare in una sola riga. Tutte le righe devono avere lo stesso numero di colonne.

## Così sì e così no

I nomi delle biblioteche e i telefoni sono inventati.

Qui i dati di una biblioteca sono spezzati su due righe.

!!! failure "Così no"

    | comune | biblioteca | telefono | data_apertura |
    | --- | --- | --- | --- |
    | Palermo | Biblioteca di esempio A | +390910000001 | 1985-03-12 |
    | Roma | Biblioteca di esempio D |  |  |
    |  |  | +390600000004 | 1998-06-01 |

!!! success "Così sì"

    | comune | biblioteca | telefono | data_apertura |
    | --- | --- | --- | --- |
    | Palermo | Biblioteca di esempio A | +390910000001 | 1985-03-12 |
    | Roma | Biblioteca di esempio D | +390600000004 | 1998-06-01 |

Vale anche al contrario: due biblioteche non stanno nella stessa riga.

## Perché

Chi riusa i dati conta e filtra per righe. Nel primo esempio le biblioteche risultano tre invece di due, e chi filtra le righe di Roma perde il telefono e la data di apertura.

## Casi particolari

### Virgole, virgolette e a capo dentro un valore

Un valore deve stare tra virgolette (`"`) se contiene il separatore, delle virgolette o un'interruzione di riga. Per gli altri valori le virgolette sono facoltative. Le virgolette dentro un valore si scrivono raddoppiate (`""`). Sono le regole della [RFC 4180](https://datatracker.ietf.org/doc/html/rfc4180), il documento di riferimento per il formato CSV.

Questa tabella

| comune | biblioteca | prestiti |
| --- | --- | --- |
| Palermo | Biblioteca di esempio A<br>Sala ragazzi | 12450 |
| Roma | Biblioteca di esempio D, sede centrale | 20310 |
| Cella Dati | Biblioteca "di esempio" C |  |

nel file CSV si scrive così:

```csv
comune,biblioteca,prestiti
Palermo,"Biblioteca di esempio A
Sala ragazzi",12450
Roma,"Biblioteca di esempio D, sede centrale",20310
Cella Dati,"Biblioteca ""di esempio"" C",
```

Il file ha cinque righe di testo, ma tre righe di dati: l'a capo tra virgolette fa parte del valore.

Senza virgolette, chi legge il file vede una riga finita a metà e una riga nuova che comincia con il resto del valore.

!!! failure "Così no: l'a capo senza virgolette"

    | comune | biblioteca | prestiti |
    | --- | --- | --- |
    | Palermo | Biblioteca di esempio A |  |
    | Sala ragazzi | 12450 |  |
    | Roma | Biblioteca di esempio D, sede centrale | 20310 |

### Spazi

Secondo la RFC 4180 gli spazi fanno parte del valore. Un valore con spazi in mezzo alle parole non ha bisogno di virgolette: `Biblioteca di esempio A` e `"Biblioteca di esempio A"` sono lo stesso valore. Per gli spazi all'inizio e alla fine vedi la [scheda 10](P10_campi_tipo_testo.md).

### Caratteri di fine riga

Ogni riga finisce con caratteri invisibili, il ritorno a capo (`CR`, *carriage return*) e l'avanzamento di linea (`LF`, *line feed*). I sistemi operativi li scrivono in modo diverso:

- **DOS e Windows:** `CR` seguito da `LF`, cioè `CRLF` o `\r\n`.
- **UNIX e sistemi simili, incluso macOS:** `LF`, cioè `\n`.

La RFC 4180 indica `CRLF`. Questa differenza può dare problemi quando si scambiano, importano o esportano file CSV fra sistemi operativi diversi.

## Come si fa nel foglio di calcolo

Non scrivere le virgolette a mano. Il programma le aggiunge da solo quando esporta il CSV e raddoppia quelle interne, come abbiamo provato con LibreOffice 25.2. Se le scrivi tu dentro la cella, diventano parte del valore.

Vedi anche: [1. Una sola riga di intestazione](P01_unica_riga_intestazione.md), [4. Righe nuove, non colonne nuove](P04_strutture_dati_verticale_orizzontale.md), [10. Metti tra virgolette il testo che lo richiede](P10_campi_tipo_testo.md).
