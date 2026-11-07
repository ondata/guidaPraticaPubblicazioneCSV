---
hide:
 - toc
# - navigation
title: Esempi di CSV italiani
---

# Esempi di CSV italiani

Tre file pubblicati da enti italiani che puoi guardare come riferimento. Per ciascuno diciamo anche cosa si potrebbe migliorare. La situazione descritta è quella del 7 novembre 2026, e i file possono cambiare.

Per ogni file abbiamo scritto uno schema in [Table Schema](https://datapackage.org/standard/table-schema/) e controllato le colonne a vista. Con lo schema si può ripetere il controllo:

```
frictionless validate file.csv --encoding utf-8 --schema file.schema.yaml
```

Senza schema `frictionless validate` guarda solo la struttura: più sotto c'è un file che risulta valido anche con un CAP di tre cifre.

## Popolazione residente, ANPR

Anagrafe nazionale della popolazione residente (ANPR). [File CSV](https://raw.githubusercontent.com/italia/anpr-opendata/main/data/popolazione%5Fresidente%5Fexport.csv), Ministero dell'Interno, 7.894 righe, licenza CC0. [Schema](../../risorse/schemi/anpr-popolazione-residente.schema.yaml).

- **Fa bene:** virgola come separatore, UTF-8, un solo codice Istat di 6 caratteri per riga, con gli zeri iniziali (`001168`). Il comune di None è scritto `NONE`, senza trasformarsi in un valore mancante. Si aggiorna ogni giorno. Il [repository](https://github.com/italia/anpr-opendata) pubblica anche un Data Package.
- **Da migliorare:** la data è `07-11-2026`, non `2026-11-07`, e i nomi sono tutti in maiuscolo. Il Data Package dichiara `COD_ISTAT_COMUNE` come numero intero, il che farebbe perdere gli zeri, e chiama `DATA ELABORAZIONE` la colonna che nel file è `DATA_ELABORAZIONE`.

## Biblioteche, Provincia di Avellino

[File CSV](https://www.provincia.avellino.it/cprvnvll/images/OpenData/Biblioteche/Biblioteche.csv), 124 righe, licenza CC BY 4.0. [Schema](../../risorse/schemi/avellino-biblioteche.schema.yaml).

- **Fa bene:** virgola come separatore, UTF-8, un codice ISIL (l'identificativo internazionale delle biblioteche) unico per ogni biblioteca, virgolette corrette dove serve (`"via Libertà, 1"`), nessun vuoto.
- **Da migliorare:** l'indirizzo sta in una cella sola, il comune è senza codice Istat, non ci sono coordinate.

## Biblioteche, Comune di Prato

[File CSV](http://odn.comune.prato.it/dataset/cd32e9d4-9641-45ec-9270-58aaaab0f0ba/resource/386fb5a6-4f7d-4f8e-9527-e5ce8034c942/download/puntidiinteressebiblioteche.csv), 26 righe, licenza CC BY 4.0. [Schema](../../risorse/schemi/prato-biblioteche.schema.yaml).

- **Fa bene:** virgola e punto decimale, latitudine e longitudine in due colonne.
- **Da migliorare:** le coordinate compaiono due volte (`X,Y` e `longitude,latitude`), l'indirizzo è abbreviato (`V.S.Caterina 17`), il sistema di riferimento non è indicato nel file e in una riga c'è uno spazio superfluo.

## Esempi didattici

Questi esempi servono a capire problemi comuni e non sono una critica ai file o agli enti che li pubblicano. Descrivono i file come erano il 7 novembre 2026, e il link porta alla copia di quel giorno su Internet Archive: nel frattempo possono essere cambiati. Tutti superano il controllo di struttura, ma ognuno mostra qualcosa che quel controllo non vede.

- **CAP senza le prime cifre.** Nello [stradario del referendum 2026 del Comune di Milano](https://web.archive.org/web/20261107162646/https://dati.comune.milano.it/dataset/645e8e6a-aff3-47ef-9dce-4d102ff471b8/resource/e1a336d2-8dd6-483f-913f-4388758dd446/download/ds2973_stradario_referendum_2026.csv) il CAP è `138` in 50.835 righe su 50.838: sembra un `20138` a cui mancano le prime due cifre. La regola è quella dei [codici come testo](P09_campi_codificati.md).
- **CAP `0`.** Nella [numerazione civica del Comune di Bergamo](https://web.archive.org/web/20261107162913/https://www.dati.lombardia.it/api/views/pcif-9jj7/rows.csv?accessType=DOWNLOAD) il CAP è `0` in 2.795 righe su 20.920: sembra uno zero al posto di un valore mancante, e si legge come un dato. La regola è quella dei [valori mancanti](P05_trattamento_valori_sconosciuti.md).
- **Codici diventati decimali.** Nei [numeri civici del Comune di Bologna](https://web.archive.org/web/20261107163325/https://opendata.comune.bologna.it/api/v2/catalog/datasets/rifter_civici_pt/exports/csv?use_labels=true) il codice della via è `16650.0`: sembra un codice trattato come numero. La copia su Internet Archive è stata salvata poco dopo la nostra e ha un ordine di righe diverso, perché il file è generato al momento, ma il difetto è lo stesso.
- **Decimale con la virgola.** Nei [numeri civici del Comune di Palermo](https://web.archive.org/web/20261107163617/https://opendata.comune.palermo.it/js/server/uploads/dataset/csv/_01042026064924.csv) le coordinate sono `13,367798`, con `;` come separatore. Il file ha il codice Istat con gli zeri e i progressivi nazionali di strada e accesso. Chi lo legge con un programma deve dichiarare la virgola come decimale, e questa guida usa il punto.

Se uno di questi file è cambiato, o se un ente preferisce che l'esempio venga aggiornato, scrivici: [apri una discussione](https://github.com/ondata/guidaPraticaPubblicazioneCSV/discussions).
