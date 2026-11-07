---
hide:
#   - navigation
title: Dizionari di dati
---


# Dizionari di dati

- Il **dizionario dei dati** è un complemento essenziale per qualsiasi serie di dati, poiché **fornisce** all'utente le **informazioni** sufficienti per elaborare e comprenderne il contenuto senza ambiguità.
- Il suo scopo è quello di **garantire** che la **struttura del *set* di dati** sia **definita in termini** facilmente **comprensibili** dagli utenti.
- **Ogni *set* di dati** pubblicabile deve **includere** il suo **dizionario di dati** come documento separato, di solito accessibile tramite un URL presente nello spazio di download dei dati.
- Il contenuto di un **dizionario di dati** può essere espresso in diversi modi, anche **come un file di testo** che **descrive il contenuto di ogni colonna** del set di dati.
- Le **caratteristiche o annotazioni** espresse nel **dizionario dei dati** sono le **proprietà** delle tabelle, **colonne**, **righe** e **celle** che compongono l'insieme di dati.
- Quello che segue è un esempio di un dizionario di dati espresso come file di testo, che può essere fornito attraverso un server web. Per esempio, tramite l'URL: `https://sito_di_esempio.it/automobili-dizionario.txt`.


## Esempio di dizionario dati espresso come file di testo

``` title="automobili-dizionario.txt"
File di dati: https://sito_di_esempio.it/automobili.csv
Descrizione: tabella con dati sulle auto d'epoca
Editore: Autore di esempio
Licenza: CC BY 4.0
Separatore: ,
Delimitatore di testo: "
Codifica: UTF-8
Colonna 1:
      Titolo: marca
      Descrizione: Questo campo contiene informazioni sulla marca e il modello di ogni veicolo.
      Tipo di dati: stringa
Colonna 2:
      Titolo: anno
      Descrizione: Questo campo contiene informazioni sull'anno di fabbricazione di ogni veicolo.
      Tipo di dati: data
Colonna 3:
      Titolo: cilindri
      Descrizione: Questo campo contiene informazioni sul numero di cilindri di ogni veicolo.
      Tipo di dati: intero
Colonna 4:
      Titolo: consumo
      Descrizione: Questo campo contiene informazioni sul consumo medio di ogni veicolo, misurato in miglia per gallone.
      Tipo di dati: decimale
Colonna 5:
      Titolo: potenza
      Descrizione: Questo campo contiene informazioni sulla potenza di ogni veicolo, misurata in CV.
      Tipo di dati: decimale
Colonna 6:
      Titolo: accelerazione
      Descrizione: Questo campo contiene il tempo di accelerazione di ogni veicolo, misurato in secondi.
      Tipo di dati: decimale
```

- È buona pratica che il **dizionario dei dati** sia espresso in un **formato *machine readable***, ad esempio [`JSON`](https://www.rfc-editor.org/rfc/rfc8259) o [`JSON-LD`](https://www.w3.org/TR/json-ld11/), utilizzando un **vocabolario standardizzato** per definire ciascuna delle caratteristiche o annotazioni su ciascuno degli elementi del file di dati.
- In alcune piattaforme Open Data, ad esempio quelle implementate con [CKAN](https://ckan.org/), il **dizionario dei dati** è specificato come una **sezione associata a ciascuna risorsa** in un set di dati.
- Per le pubbliche amministrazioni italiane, i metadati del dataset seguono il profilo [DCAT-AP_IT](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-15) e, per i dati territoriali, le [Linee guida RNDT](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-16). Il dizionario dei dati non sostituisce questi metadati.
- Dichiara la **licenza** nei metadati del dataset. Per i dati aperti di una pubblica amministrazione il riferimento è la CC BY 4.0, oppure CC0: le [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/capitolo-6.html#req-20) chiedono di motivare formalmente una scelta più restrittiva, e sconsigliano licenze locali come la IODL.
- Quando si impostano i **valori delle proprietà**, è consigliabile usare un **linguaggio chiaro e conciso**, poiché gli utenti finali dei dati potrebbero non avere necessariamente familiarità con i dati.
## Schema e validazione

Uno schema è il dizionario dei dati scritto in un file che i programmi sanno leggere: dice di che tipo è ogni colonna e quali vincoli ha. Così un programma può controllare il CSV da solo e indicare riga e colonna sbagliate. Per chi lavora con un foglio di calcolo basta il dizionario qui sopra; lo schema è il passo successivo.

Il formato che consigliamo è [Table Schema](https://datapackage.org/standard/table-schema/), del progetto Frictionless Data, indicato a titolo di esempio dalle [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/capitolo-5.html#sec-modellazione-e-documentazione). Non è un obbligo.

``` yaml title="automobili.schema.yaml"
fields:
  - {name: marca, type: string, title: Marca e modello, constraints: {required: true}}
  - {name: anno, type: year, title: Anno di fabbricazione}
  - {name: cilindri, type: integer}
  - {name: consumo, type: number, description: Consumo medio in miglia per gallone}
  - {name: potenza, type: number, description: Potenza in CV}
  - {name: accelerazione, type: number, description: Tempo di accelerazione in secondi}
missingValues: [""]
```

Il controllo si fa con [Frictionless Framework](./linee_guida_pubblicazione/Cassetta_attrezzi.md):

```
frictionless validate automobili.csv --encoding utf-8 --schema automobili.schema.yaml
```

Se in una riga l'anno è `settanta`, il comando segnala un `type-error` con il numero di riga e il nome della colonna. Più schemi e i loro file si possono raccogliere in un [Data Package](https://datapackage.org/standard/data-package/). La pagina [Esempi di CSV italiani](./linee_guida_pubblicazione/Esempi_dati_CSV.md) ha tre schemi di file reali da cui partire.

## CSVW, lo standard del W3C

[CSV on the Web](https://www.w3.org/TR/tabular-data-model/) (CSVW) è la Raccomandazione del W3C del 2015 per descrivere i file CSV. Resta valida e stabile, ma non è più sviluppata: il suo [Community Group](https://www.w3.org/community/csvw/) ha chiuso il 21 maggio 2026.

- Il W3C raccomanda un [modello per i dati tabulari](https://www.w3.org/TR/tabular-data-model/) e propone un [vocabolario per la descrizione di queste proprietà](https://www.w3.org/TR/tabular-metadata/).
- Il vocabolario W3C è molto esaustivo, tuttavia, ci sono un certo numero di proprietà che è consigliabile prendere in considerazione per qualsiasi file tabellare:
    - Per le tabelle:
         - Titolo della tabella `["dc:title"]`
         - Descrizione `["dc:description"]`
         - Titolare del dato `["dc:creator"]`
         - URL della tabella `["url"]`
    - Per le colonne:
         - Nome della colonna `["name"]`
         - Titolo della colonna `["titles"]`
         - Descrizione `["dc:description"]`
         - Tipo di dato: `["datatype"]`
- Inoltre, è possibile annotare attraverso l'uso di diverse proprietà, altri metadati: ordine delle colonne, valori attesi, valori richiesti, valori univoci, chiavi esterne, elenchi di valori, formati, restrizioni, validazioni, istruzioni per la trasformazione del CSV in un altro formato.
- Quello che segue è un esempio di un dizionario di dati espresso in formato JSON che può essere reso disponibile tramite un server web. Per esempio, tramite l'URL: `https://sito_di_esempio.it/automobili.csv-metadata.json`.


## Esempio di dizionario dati in formato json-ld

``` json title="automobili.csv-metadata.json"
{
  "@context": "http://www.w3.org/ns/csvw",
  "@type": "Table",
  "url": "https://sito_di_esempio.it/automobili.csv",
  "dc:description": "Tabella con dati sulle auto d'epoca",
  "dc:creator": "Autore dell'esempio",
  "tableSchema": {
    "columns": [
      {
        "name": "marca",
        "titles": "marca",
        "dc:description": "Questo campo contiene informazioni sulla marca e il modello di ogni veicolo",
        "datatype": "string"
      },
      {
        "name": "anno",
        "titles": "anno",
        "dc:description": "Questo campo contiene informazioni su l'anno di fabbricazione di ogni veicolo",
        "datatype": "gYear"
      },
      {
        "name": "cilindri",
        "titles": "cilindri",
        "dc:description": "Questo campo contiene informazioni sul numero di cilindri di ogni veicolo",
        "datatype": "integer"
      },
      {
        "name": "consumo",
        "titles": "consumo",
        "dc:description": "Questo campo contiene informazioni sul consumo medio di carburante di ogni veicolo, misurato in miglia per gallone",
        "datatype": "decimal"
      },
      {
        "name": "potenza",
        "titles": "potenza",
        "dc:description": "Questo campo contiene informazioni sulla potenza di ogni veicolo, misurata in CV",
        "datatype": "decimal"
      },
      {
        "name": "accelerazione",
        "titles": "accelerazione",
        "dc:description": "Questo campo contiene il tempo di accelerazione di ogni veicolo, misurato in secondi",
        "datatype": "decimal"
      }
    ]
  }
}

```

Il dizionario dei dati mostrato come esempio è associato al set di dati mostrato in questa guida.

- Tra le altre proprietà, il nome di ogni colonna viene descritto utilizzando la proprietà `name`.
- La proprietà `titles` è usata per definire un titolo *human-readable* per la colonna.
- Il `titles` della colonna può essere accompagnato da un codice di lingua in modo che la riga di intestazione possa essere descritta in diverse lingue.
- La proprietà `datatype` è usata per descrivere il tipo di dato in cui è espressa la colonna corrispondente.
- La proprietà `dc:description` permette di includere un testo descrittivo del contenuto di ogni colonna.
- Strumenti come quelli descritti nella sezione [Cassetta degli attrezzi per i file CSV](./linee_guida_pubblicazione/Cassetta_attrezzi.md) di questa guida, per esempio CSVlint, permettono di controllare la coerenza del dataset confrontando il contenuto del dizionario dei dati e la struttura del file dei dati.
- Tra gli altri controlli, è possibile convalidare il numero di colonne e i loro nomi, il tipo di valori ammessi, se questi valori devono essere univoci o se ci sono collegamenti di questi valori ad altre tabelle (chiavi esterne).
