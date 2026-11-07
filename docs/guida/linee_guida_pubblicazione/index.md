---
hide:
 - toc
# - navigation
title: Le 15 regole in una pagina
---

# Le 15 regole in una pagina

Una sola tabella per file, separatore virgola, codifica UTF-8, e un [dizionario dei dati](../dizionario_dati.md) che spiega ogni colonna.

<div class="regole" markdown>

| N. | Regola | Così sì | Così no |
| --- | --- | --- | --- |
| 1 | [Una sola riga di intestazione, nella prima riga](P01_unica_riga_intestazione.md) | `marca,anno,vendite` | titolo sopra i nomi delle colonne |
| 2 | [Una riga per ogni record, con lo stesso numero di colonne](P02_singolo_record_riga.md) | `Palermo,636783` | un record spezzato su due righe |
| 3 | [Nomi di colonna brevi, minuscoli, senza spazi né accenti](P03_denominazione_colonne.md) | `data_lancio` | `Data di lancio`, `Cil.` |
| 4 | [Una colonna per variabile: i dati nuovi vanno in righe](P04_strutture_dati_verticale_orizzontale.md) | `marca,anno,domanda` | `marca,1972,1973` |
| 5 | [Se un valore manca, cella vuota e spiegazione nel dizionario](P05_trattamento_valori_sconosciuti.md) | `Palermo,,2023` | `NA`, oppure `0` al posto del vuoto |
| 6 | [Niente totali e subtotali](P06_subtotali_totali_raggruppamenti.md) | solo righe di dettaglio | una riga `Totale` |
| 7 | [Un solo tipo di dato per colonna, unità nel nome](P07_tipi_dati.md) | `potenza_cv` con `130` | `130 CV` |
| 8 | [La stessa cosa sempre allo stesso modo, meglio con un codice standard](P08_standardizzazione_valori_campi.md) | `Reggio nell'Emilia`, `035033` | `Reggio Emilia`, `35033` |
| 9 | [Se usi un codice, affiancagli la descrizione](P09_campi_codificati.md) | `M,Manuale` | solo `M` |
| 10 | [Testo con separatori, a capo o virgolette: tra virgolette](P10_campi_tipo_testo.md) | `"via Libertà, 1"` | `via Libertà, 1` |
| 11 | [Numeri con il punto decimale, senza migliaia né simboli](P11_campi_tipo_numerico.md) | `1230.50` | `1.230,50`, `€50` |
| 12 | [Date nel formato anno-mese-giorno](P12_campi_tipo_data.md) | `2019-09-30` | `30/09/19` |
| 13 | [Telefoni meglio in formato internazionale, senza separatori](P13_campi_tipo_numero_telefonico.md) | `+390515270001` | `051 527 0001` |
| 14 | [Indirizzi divisi in colonne](P14_campi_tipo_indirizzo_postale.md) | `Via,Roma,10` | `Via Roma n° 10, Milano` |
| 15 | [Latitudine e longitudine in due colonne, in gradi decimali, con il sistema di riferimento dichiarato](P15_campi_con_coordinate_geografiche.md) | `38.1157` | `43° 14' 04"` |

</div>

Prima di pubblicare, apri il file con un editor di testo, controlla i [dati personali](Dati_personali.md) e validalo con uno [strumento](Cassetta_attrezzi.md).

<div class="regole-altro" markdown>

## Approfondimenti

- [Esportare un CSV da Excel o LibreOffice](Linee_guida_importazione_esportazione.md)
- [Tassonomie ed elenchi di codici comunemente usati](Tassonomie_elenchi_codici.md)
- [Considerazioni sull'archiviazione dei file](Considerazioni_archiviazione.md)
- [Prima di pubblicare i dati personali](Dati_personali.md)
- [Cassetta degli attrezzi per i file CSV](Cassetta_attrezzi.md)
- [Esempi di CSV italiani](Esempi_dati_CSV.md)
- [Link utili](Link_utili.md)

</div>
