---
hide:
   - navigation
title: Dizionari di dati
---


# Dizionari di dati

Il dizionario dei dati è un complemento essenziale per qualsiasi serie di dati, poiché fornisce all'utente dei dati informazioni sufficienti per elaborare e comprendere il suo contenuto senza ambiguità.

- Il suo scopo è quello di garantire che la struttura del set di dati sia definita in termini facilmente comprensibili dagli utenti.
- Ogni set di dati pubblicabile deve includere il suo dizionario di dati come documento separato, di solito accessibile tramite un URL dal punto di download del file di dati.
- Il contenuto di un dizionario di dati può essere espresso in diversi modi, anche come un file di testo che descrive il contenuto di ogni colonna del set di dati.
- Le caratteristiche o annotazioni espresse nel Dizionario dei dati sono le proprietà delle tabelle, colonne, righe e celle che compongono l'insieme di dati.
- Quello che segue è un esempio di un dizionario di dati espresso come un file di testo che può essere fornito attraverso un server web. Per esempio, tramite l'URL: http://example.org/automoviles.csv-metadata.txt.


## Esempio di dizionario dei dati espresso come file di testo

```
File di dati: [`automobili.csv`](../risorse/tabelle/automobili.csv)
Descrizione: tabella con dati sulle auto d'epoca
Editore: Autore di esempi
Colonna 1:
      Titolo: marchio
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
      Descrizione: Questo campo contiene informazioni sul consumo medio di ogni veicolo, misurato in litri / 100 km.
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


È buona pratica che il dizionario dei dati sia espresso in un formato *machine readable*, ad esempio `JSON` o `JSON-LD`, utilizzando un vocabolario standardizzato per definire ciascuna delle caratteristiche o annotazioni su ciascuno degli elementi del file di dati.

- In alcune piattaforme Open Data, ad esempio quelle implementate con CKAN, il dizionario dei dati è specificato come una sezione associata a ciascuna risorsa in un set di dati.
- Secondo il Technical Standard for Information Resources Interoperability (TSI), il modo di specificare il modello di dati è usando la proprietà "`dct:relation`" nei metadati di distribuzione delle risorse del dataset.
- Quando si impostano i valori delle proprietà, è consigliabile usare un linguaggio chiaro e conciso, poiché gli utenti finali dei dati potrebbero non avere necessariamente familiarità con i dati.
- Il W3C raccomanda un modello per i dati tabulari e propone un vocabolario per la descrizione di queste proprietà.
- Il vocabolario W3C è molto esaustivo, tuttavia, ci sono un certo numero di proprietà che è consigliabile prendere in considerazione per qualsiasi file tabellare:

- Per le righe:
     - Titolo della tabella ["`dc:title`"].
     - Descrizione ["`dc:description`"]
     - Editore ["`dc:creator`"].
     - Posizione del file da descrivere ["`url`"].

- Per le colonne:
     - Colonna name["`name`"]
     - Titolo della colonna ["`titoli`"].
     - Descrizione["`dc:description`"]
     - Tipi di dati: ["`datatype`"].

- Inoltre, è possibile annotare attraverso l'uso di diverse proprietà, tra gli altri metadati, quanto segue: ordine delle colonne, valori attesi, valori richiesti, valori unici, chiavi esterne, elenchi di valori, lingue di stringa, formati, restrizioni, validazioni, istruzioni per la trasformazione del CSV in un altro formato.
- Quello che segue è un esempio di un dizionario di dati espresso come schema in formato JSON che può essere fornito tramite un server web. Per esempio, tramite l'URL: [http://example.org/automoviles.csv-metadata.json](http://example.org/automoviles.csv-metadata.json).


## Esempio di dizionario di dati usando il formato json-ld
```
{
"@context": "http://www.w3.org/ns/csvw", "@type": "Table",
"url": "http://example.org/automoviles.csv", "dc:description": "Tabella con dati sulle auto classiche" "dc:creator": "Autore dell'esempio".
"tableSchema": {
                  "colonne": [{
                                 "nome": "identificatore",
                                 "titoli": "marchio",
                                 "dc:description": "Questo campo contiene informazioni sulla marca e il modello di ogni veicolo".
                                 "datatype": "string" },
                                 {"nome": "annio",
                                 "titoli": "anno",
                                 "dc:description": "Questo campo contiene informazioni su
                                 l'anno di fabbricazione di ogni veicolo".
                                 "datatype": {
                                 "base": "data". ,
                                 "formato": "aaaa"}},
                                 {"nome": "cilindri",
                                 "titoli": cilindri",
                                 "dc:description": "Questo campo contiene informazioni sul numero di cilindri di ogni veicolo".
                                 "datatype": "integer" },
                                 {"nome": "consumo",
                                 "titoli": "consumo",
                                 "dc:description": "Questo campo contiene informazioni sul consumo medio di carburante di ogni veicolo, misurato in litri / 100 km".
                                 "datatype": "decimal" },
                                 {"nome": "potenza",
                                 "titoli": "potenza",
                                 "dc:description": "Questo campo contiene informazioni sulla potenza di ogni veicolo, misurata in CV". "datatype": "decimal" },
                                 {"nome": "accelerazione", "titoli": "accelerazione",
                                 "dc:description": "Questo campo contiene dati sull'accelerazione di ogni veicolo misurata in m/sec2" "datatype": "decimal" "dc:description": "Questo campo contiene dati sull'accelerazione di ogni veicolo misurata in m/sec2" "datatype": "decimal".
                                 }}]
}
```

Il dizionario dei dati mostrato come esempio è associato al set di dati mostrato in questa guida.

- Tra le altre proprietà, il nome di ogni colonna viene descritto utilizzando la proprietà "`name`".
- L'uso della proprietà "`title`" è usato per specificare la riga di intestazione della tabella. L'assenza di questa proprietà indica che la tabella non ha una riga di intestazione.
- Questa intestazione per ogni colonna può essere accompagnata da un codice di lingua in modo che la riga di intestazione possa essere espressa in diverse lingue.
- La proprietà "`datatype`" è usata per descrivere i tipi di dati in cui il <kbd>  manca una parola </kbd>
esprime ogni valore nella colonna corrispondente.
- La proprietà "description" permette di includere un testo descrittivo del contenuto di ogni colonna.
- Strumenti come quelli descritti nella sezione "Toolbox forCSVfiles" di questa guida, per esempio CSVlint, permettono di controllare la coerenza del dataset confrontando il contenuto del dizionario dei dati e la struttura del file dei dati.
- Tra gli altri controlli, è possibile convalidare il numero di colonne e i loro nomi, il tipo di valori ammessi, se questi valori devono essere unici o se ci sono collegamenti di questi valori ad altre tabelle (chiavi esterne).

