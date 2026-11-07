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
| 1 | [Una sola riga di intestazione, nella prima riga](P01_unica_riga_intestazione.md) | `comune,anno,prestiti` | titolo sopra i nomi delle colonne |
| 2 | [Una riga per ogni record, con lo stesso numero di colonne](P02_singolo_record_riga.md) | `Palermo,2023,12450` | un record spezzato su due righe |
| 3 | [Nomi di colonna chiari, meglio minuscoli e senza spazi né accenti](P03_denominazione_colonne.md) | `data_apertura` | `Data di apertura`, `Ap.` |
| 4 | [Righe nuove, non colonne nuove, quando i dati crescono](P04_strutture_dati_verticale_orizzontale.md) | `comune,anno,prestiti` | `comune,2022,2023` |
| 5 | [Se un valore manca, cella vuota e spiegazione nel dizionario](P05_trattamento_valori_sconosciuti.md) | `Cella Dati,2023,` | `NA`, oppure `0` al posto del vuoto |
| 6 | [Niente totali e subtotali](P06_subtotali_totali_raggruppamenti.md) | solo righe di dettaglio | una riga `Totale` |
| 7 | [Un solo tipo di dato per colonna, unità nel nome](P07_tipi_dati.md) | `spesa_acquisti_euro` con `300.00` | `300 euro` |
| 8 | [La stessa cosa sempre allo stesso modo, meglio con un codice standard](P08_standardizzazione_valori_campi.md) | `Reggio nell'Emilia`, `035033` | `Reggio Emilia`, `35033` |
| 9 | [Se usi un codice, affiancagli la descrizione](P09_campi_codificati.md) | `082053,Palermo` | solo `082053` |
| 10 | [Testo con virgole, a capo o virgolette: tra virgolette](P10_campi_tipo_testo.md) | `"Biblioteca, sede centrale"` | `Biblioteca, sede centrale` |
| 11 | [Numeri con il punto decimale, senza migliaia né simboli](P11_campi_tipo_numerico.md) | `8200.50` | `8.200,50`, `€ 8200` |
| 12 | [Date nel formato anno-mese-giorno](P12_campi_tipo_data.md) | `1985-03-12` | `12/03/85` |
| 13 | [Telefoni meglio in formato internazionale, senza separatori](P13_campi_tipo_numero_telefonico.md) | `+390910000001` | `091 000 0001` |
| 14 | [Indirizzi meglio divisi in colonne](P14_campi_tipo_indirizzo_postale.md) | `Via,Roma,10` | `Via Roma n. 10, Palermo` |
| 15 | [Latitudine e longitudine in due colonne, in gradi decimali, con il sistema di riferimento dichiarato](P15_campi_con_coordinate_geografiche.md) | `38.1157` | `38° 06' 57"` |

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
