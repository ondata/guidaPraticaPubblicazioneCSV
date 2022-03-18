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
- Quello che segue è un esempio di un dizionario di dati espresso come file di testo, che può essere fornito attraverso un server web. Per esempio, tramite l'URL: `https://sito_di_esempio.it/automobili.csv-metadata.txt`.


## Esempio di dizionario dati espresso come file di testo

``` title="automobili.csv-metadata.txt"
File di dati: https://sito_di_esempio.it/automobili.csv
Descrizione: tabella con dati sulle auto d'epoca
Editore: Autore di esempio
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
      Descrizione: Questo campo contiene informazioni sul consumo medio di ogni veicolo, misurato in litri/100 km.
      Tipo di dati: decimale
Colonna 5:
      Titolo: potenza
      Descrizione: Questo campo contiene informazioni sulla potenza di ogni veicolo, misurata in CV.
      Tipo di dati: decimale
Colonna 6:
      Titolo: accelerazione
      Descrizione: Questo campo contiene dati sull'accelerazione di ogni veicolo, misurata in m/sec2.
      Tipo di dati: decimale
```

- È buona pratica che il **dizionario dei dati** sia espresso in un **formato *machine readable***, ad esempio [`JSON`](https://www.w3schools.com/js/js_json_intro.asp) o [`JSON-LD`](https://www.w3.org/TR/json-ld11/), utilizzando un **vocabolario standardizzato** per definire ciascuna delle caratteristiche o annotazioni su ciascuno degli elementi del file di dati.
- In alcune piattaforme Open Data, ad esempio quelle implementate con [CKAN](https://ckan.org/), il **dizionario dei dati** è specificato come una **sezione associata a ciascuna risorsa** in un set di dati.
- Secondo la "[Norma Técnica de Interoperabilidad de Reutilización de Recursos de Información](https://datos.gob.es/en/documentacion/norma-tecnica-de-interoperabiliad-de-reutilizacion-de-recursos-de-informacion)" (NTI), il modo di specificare il **modello di dati** è usare la **proprietà "`dct:relation`" nei metadati** di distribuzione delle risorse del dataset.
- Quando si impostano i **valori delle proprietà**, è consigliabile usare un **linguaggio chiaro e conciso**, poiché gli utenti finali dei dati potrebbero non avere necessariamente familiarità con i dati.
- Il W3C raccomanda un [modello per i dati tabulari](https://www.w3.org/TR/tabular-metadata/) e propone un [vocabolario per la descrizione di queste proprietà](https://www.w3.org/TR/tabular-metadata/).
- Il vocabolario W3C è molto esaustivo, tuttavia, ci sono un certo numero di proprietà che è consigliabile prendere in considerazione per qualsiasi file tabellare:
    - Per le tabelle:
         - Titolo della tabella `["dc:title"]`
         - Descrizione `["dc:description"]`
         - Titolare del dato `["dc:creator"]`
         - URL della tabella `["url"]`
    - Per le colonne:
         - Nome della colonna `["name"]`
         - Titolo della colonna `["titoli"]`
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
    "colonne": [
      {
        "name": "identificatore",
        "titles": "marca",
        "dc:description": "Questo campo contiene informazioni sulla marca e il modello di ogni veicolo",
        "datatype": "string"
      },
      {
        "name": "anno",
        "titles": "anno",
        "dc:description": "Questo campo contiene informazioni su l'anno di fabbricazione di ogni veicolo",
        "datatype": {
          "base": "data",
          "format": "yyyy"
        }
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
        "dc:description": "Questo campo contiene informazioni sul consumo medio di carburante di ogni veicolo, misurato in litri/100 km",
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
        "dc:description": "Questo campo contiene dati sull'accelerazione di ogni veicolo misurata in m/sec2",
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
- Strumenti come quelli descritti nella sezione ["Strumenti per file CSV"](strumenti_file_CSV.md) di questa guida, per esempio CSVlint, permettono di controllare la coerenza del dataset confrontando il contenuto del dizionario dei dati e la struttura del file dei dati.
- Tra gli altri controlli, è possibile convalidare il numero di colonne e i loro nomi, il tipo di valori ammessi, se questi valori devono essere univoci o se ci sono collegamenti di questi valori ad altre tabelle (chiavi esterne).