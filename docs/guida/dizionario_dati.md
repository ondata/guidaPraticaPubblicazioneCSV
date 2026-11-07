---
hide:
#   - navigation
title: Il dizionario dei dati
---

# Il dizionario dei dati

Il dizionario dei dati è la legenda della tabella: dice che cosa contiene ogni colonna, di che tipo è, in quale unità di misura, e come è fatto il file. Con il dizionario, chi riusa i dati li capisce senza dover chiedere nulla a chi li ha pubblicati.

Ogni dataset deve avere il suo dizionario, in un documento separato dal file dei dati e scaricabile accanto a esso.

## Il dizionario come tabella

Questo è il punto di partenza, e per chi lavora con un foglio di calcolo basta. Il dizionario si prepara in un foglio a parte, si salva come file a sé e si pubblica accanto ai dati.

L'esempio descrive il [dataset delle biblioteche](../risorse/esempi/biblioteche.csv) usato in tutta la guida. Nome della biblioteca, telefoni, spese e prestiti sono inventati; codici Istat e nomi dei comuni sono veri.

Prima le informazioni sul file:

| Voce | Valore |
| --- | --- |
| File di dati | `biblioteche.csv` |
| Descrizione | Biblioteche comunali, dati di esempio. Una riga per ogni biblioteca, riferita all'anno indicato |
| Licenza | CC BY 4.0 |
| Separatore | `,` |
| Delimitatore di testo | `"` |
| Codifica | UTF-8 |

Le [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/allegato-B.html#csv) raccomandano di dichiarare il separatore e il delimitatore di testo. Dichiarare anche la codifica evita a chi legge di doverla indovinare.

Poi una riga per ogni colonna:

| Colonna | Descrizione | Tipo | Unità di misura | Valori mancanti |
| --- | --- | --- | --- | --- |
| `codice_istat_comune` | Codice Istat del comune, elenco SITUAS al 2026-11-07 | testo |  |  |
| `comune` | Nome del comune | testo |  |  |
| `biblioteca` | Nome della biblioteca | testo |  |  |
| `dug` | Denominazione urbanistica generica | testo |  |  |
| `denominazione` | Denominazione della strada | testo |  |  |
| `civico` | Numero civico | numero intero |  |  |
| `esponente` | Esponente del civico | testo |  | cella vuota = nessun esponente |
| `cap` | Codice di avviamento postale | testo |  |  |
| `telefono` | Telefono della biblioteca in formato internazionale | testo |  | cella vuota = non disponibile |
| `data_apertura` | Data di apertura della biblioteca | data (AAAA-MM-GG) |  |  |
| `anno` | Anno a cui si riferiscono prestiti e spesa | anno |  |  |
| `prestiti` | Prestiti effettuati nell'anno | numero intero | prestiti | cella vuota = dato non rilevato |
| `spesa_acquisti_euro` | Spesa per acquisti di libri nell'anno | numero decimale | euro (EUR) |  |
| `latitudine` | Latitudine in gradi decimali | numero decimale | gradi (WGS84 EPSG:4326) |  |
| `longitudine` | Longitudine in gradi decimali | numero decimale | gradi (WGS84 EPSG:4326) |  |

Lo stesso dizionario si scarica come [file CSV](../risorse/esempi/biblioteche-dizionario.csv). Va bene anche un semplice file di testo con le stesse informazioni.

Tre consigli per riempirlo:

- **Descrizioni.** Usa frasi brevi e chiare: chi legge può non conoscere i tuoi dati.
- **Celle vuote.** Spiega che cosa significa una [cella vuota](linee_guida_pubblicazione/P05_trattamento_valori_sconosciuti.md) in quella colonna.
- **Codici.** Indica la data degli [elenchi di codici](linee_guida_pubblicazione/Tassonomie_elenchi_codici.md) che hai usato, perché i codici cambiano nel tempo.

## Dizionario, metadati e licenza

Il dizionario non sostituisce i metadati del dataset. Per le pubbliche amministrazioni italiane i metadati seguono il profilo [DCAT-AP_IT](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-15) e, per i dati territoriali, le [Linee guida RNDT](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-16).

La licenza si dichiara nei metadati del dataset. Per i dati aperti di una pubblica amministrazione il riferimento è la CC BY 4.0, oppure CC0: le [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/capitolo-6.html#req-21) chiedono di motivare formalmente una licenza diversa, e sconsigliano licenze locali come la IODL.

In alcune piattaforme di dati aperti, per esempio quelle basate su [CKAN](https://ckan.org/), il dizionario è una sezione associata a ciascuna risorsa del dataset.

## Per renderlo leggibile dai programmi

Da qui in poi la pagina è per chi usa il terminale o coordina i dati. Non è una condizione per pubblicare un buon CSV.

Uno schema è il dizionario dei dati scritto in un file che i programmi sanno leggere: dice di che tipo è ogni colonna e quali vincoli ha. Così un programma può controllare il CSV da solo e indicare riga e colonna sbagliate. Qui sotto ci sono due formati, e nessuno dei due è un obbligo.

### Table Schema

Il formato che consigliamo è [Table Schema](https://datapackage.org/standard/table-schema/), del progetto Frictionless Data, indicato a titolo di esempio dalle [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/capitolo-5.html#sec-modellazione-e-documentazione).

``` yaml title="biblioteche.schema.yaml"
fields:
  - {name: codice_istat_comune, type: string, title: "Codice Istat del comune, elenco SITUAS al 2026-11-07", constraints: {required: true, pattern: "[0-9]{6}"}}
  - {name: comune, type: string, constraints: {required: true}}
  - {name: biblioteca, type: string, constraints: {required: true}}
  - {name: dug, type: string, title: Denominazione urbanistica generica}
  - {name: denominazione, type: string, title: Denominazione della strada}
  - {name: civico, type: integer}
  - {name: esponente, type: string}
  - {name: cap, type: string, title: Codice di avviamento postale, constraints: {pattern: "[0-9]{5}"}}
  - {name: telefono, type: string, constraints: {pattern: "\\+[0-9]{8,15}"}}
  - {name: data_apertura, type: date}
  - {name: anno, type: year, title: Anno a cui si riferiscono prestiti e spesa}
  - {name: prestiti, type: integer, constraints: {minimum: 0}}
  - {name: spesa_acquisti_euro, type: number, description: Spesa per acquisti di libri nell'anno in euro}
  - {name: latitudine, type: number, description: Gradi decimali in WGS84 (EPSG 4326)}
  - {name: longitudine, type: number, description: Gradi decimali in WGS84 (EPSG 4326)}
missingValues: [""]
```

Il file si [scarica qui](../risorse/esempi/biblioteche.schema.yaml). Table Schema non ha una proprietà per l'unità di misura: se serve, sta nel nome della colonna e in `description`.

Il controllo si fa con [Frictionless Framework](linee_guida_pubblicazione/Cassetta_attrezzi.md):

```
frictionless validate biblioteche.csv --encoding utf-8 --schema biblioteche.schema.yaml
```

Su questo file il risultato è `VALID`. Se nella prima biblioteca l'anno diventa `duemilaventitre`, il comando segnala un `type-error` con il numero di riga e il nome della colonna. Se al codice `082053` cade lo zero iniziale, segnala un `constraint-error`, perché il valore non rispetta il vincolo di 6 cifre.

Più schemi e i loro file si possono raccogliere in un [Data Package](https://datapackage.org/standard/data-package/). La pagina [Esempi di CSV italiani](linee_guida_pubblicazione/Esempi_dati_CSV.md) ha tre schemi di file reali da cui partire.

### CSVW, lo standard del W3C

[CSV on the Web](https://www.w3.org/TR/tabular-data-model/) (CSVW) è la Raccomandazione del W3C del 2015 per descrivere i file CSV. Resta valida e stabile, ma non è più sviluppata: il suo [Community Group](https://www.w3.org/community/csvw/) ha chiuso il 21 maggio 2026. Il W3C definisce un [modello per i dati tabellari](https://www.w3.org/TR/tabular-data-model/) e un [vocabolario per descriverli](https://www.w3.org/TR/tabular-metadata/), in [JSON](https://www.rfc-editor.org/rfc/rfc8259) e [JSON-LD](https://www.w3.org/TR/json-ld11/).

Questo è il file che descrive le biblioteche. Va salvato nella stessa cartella del CSV: `url` indica il file dei dati.

``` json title="biblioteche.csv-metadata.json"
{
  "@context": ["http://www.w3.org/ns/csvw", {"@language": "it"}],
  "url": "biblioteche.csv",
  "dc:title": "Biblioteche comunali, dati di esempio",
  "dc:description": "Dati inventati a scopo di esempio. Una riga per ogni biblioteca, riferita all'anno indicato.",
  "dc:creator": "onData",
  "dc:license": {"@id": "https://creativecommons.org/licenses/by/4.0/"},
  "dialect": {"delimiter": ",", "quoteChar": "\"", "encoding": "utf-8", "header": true},
  "tableSchema": {
    "columns": [
      {"name": "codice_istat_comune", "titles": "codice_istat_comune", "dc:description": "Codice Istat del comune, elenco SITUAS al 2026-11-07", "required": true, "datatype": {"base": "string", "format": "[0-9]{6}"}},
      {"name": "comune", "titles": "comune", "dc:description": "Nome del comune", "required": true, "datatype": "string"},
      {"name": "biblioteca", "titles": "biblioteca", "dc:description": "Nome della biblioteca", "required": true, "datatype": "string"},
      {"name": "dug", "titles": "dug", "dc:description": "Denominazione urbanistica generica", "datatype": "string"},
      {"name": "denominazione", "titles": "denominazione", "dc:description": "Denominazione della strada", "datatype": "string"},
      {"name": "civico", "titles": "civico", "dc:description": "Numero civico", "datatype": "integer"},
      {"name": "esponente", "titles": "esponente", "dc:description": "Esponente del civico. Cella vuota: nessun esponente", "datatype": "string"},
      {"name": "cap", "titles": "cap", "dc:description": "Codice di avviamento postale", "datatype": {"base": "string", "format": "[0-9]{5}"}},
      {"name": "telefono", "titles": "telefono", "dc:description": "Telefono della biblioteca in formato internazionale. Cella vuota: non disponibile", "datatype": {"base": "string", "format": "\\+[0-9]{8,15}"}},
      {"name": "data_apertura", "titles": "data_apertura", "dc:description": "Data di apertura della biblioteca", "datatype": "date"},
      {"name": "anno", "titles": "anno", "dc:description": "Anno a cui si riferiscono prestiti e spesa", "datatype": "gYear"},
      {"name": "prestiti", "titles": "prestiti", "dc:description": "Prestiti effettuati nell'anno. Cella vuota: dato non rilevato", "datatype": {"base": "integer", "minimum": 0}},
      {"name": "spesa_acquisti_euro", "titles": "spesa_acquisti_euro", "dc:description": "Spesa per acquisti di libri nell'anno, in euro", "datatype": "decimal"},
      {"name": "latitudine", "titles": "latitudine", "dc:description": "Latitudine in gradi decimali, WGS84 (EPSG:4326)", "datatype": "decimal"},
      {"name": "longitudine", "titles": "longitudine", "dc:description": "Longitudine in gradi decimali, WGS84 (EPSG:4326)", "datatype": "decimal"}
    ]
  }
}
```

Il file si controlla con la libreria [csvw](https://pypi.org/project/csvw/):

```
uvx --from csvw csvwvalidate biblioteche.csv-metadata.json
```

Il comando risponde `OK` o `FAIL`; con `-v` indica il valore sbagliato, non la riga. Nella versione 4.2.0 non controlla le colonne `gYear`.

Conviene compilare almeno queste proprietà:

- **Per la tabella.** `url` (il file), `dc:title` (titolo), `dc:description` (descrizione), `dc:creator` (titolare del dato), `dc:license` (licenza), `dialect` (separatore, delimitatore, codifica, intestazione).
- **Per la colonna.** `name` (nome), `titles` (titolo per chi legge, che può portare anche un codice di lingua), `dc:description` (descrizione), `datatype` (tipo di dato).

Con altre proprietà si possono annotare valori obbligatori (`required`), valori ammessi, formati, chiavi primarie ed esterne verso altre tabelle.
