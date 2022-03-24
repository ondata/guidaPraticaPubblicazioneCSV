---
hide:
 - toc
# - navigation
title: Dove trovare buoni esempi di dati in CSV
---

Quella che segue è una descrizione di due iniziative che pubblicano set di dati aperti, di elevata qualità, disponibili in formato `CSV`:

- [Datahub.io](https://datahub.io/)
- [Kaggle.com](https://www.kaggle.com/)

In queste piattaforme è rilevante la qualità del modo in cui i dati vengono pubblicati, data la forte comprensione della natura multi-scopo dell'uso dei dati e il trattamento professionale dei dati che è al centro di entrambe le iniziative.
Datahub, si distingue per l'implementazione di un supporto completo per la trasformazione, la convalida e la pubblicazione di dati di qualità e Kaggle è una delle più importanti risorse di set di dati e conoscenze che effettuano una analisi professionale dei dati di riferimento.
Entrambe le iniziative sono esempi di buone pratiche nel trattamento dei file `CSV` che possono essere presi in considerazione quando si tratta di processi di preparazione e pubblicazione di Open Data.

## Datahub.io

Datahub è una piattaforma web-based che supporta flussi di lavoro end-to-end per la preparazione e la pubblicazione di Open Data. È progettato per preparare, catalogare e pubblicare dati di alta qualità utilizzando il toolkit Frictionless Data.
Il Frictionless Data toolbox[^1] è una raccolta di specifiche e applicazioni per la preparazione di file di dati, incluse le Goodtables, descritte nel capitolo [Cassetta degli attrezzi per i file CSV](../linee_guida_pubblicazione/Cassetta_attrezzi.md) di questa guida.
 Datahub contiene collezioni di dati di alto valore conformi agli Open Data, come: cambiamenti climatici, dati e indicatori economici, statistiche, logistica, documenti aziendali provenienti da fonti ufficiali.
 Ogni voce di dati disponibile contiene una serie di elementi per visualizzare le proprietà del dataset (schema e risorse di dati), opzioni per scaricare i dati in vari formati tra cui CSV, viste delle tabelle di dati e semplici visualizzazioni.
 Fornisce anche un accesso diretto ai dati di importazione utilizzando una varietà di strumenti comunemente usati nel contesto professionale: R, Python, JavaScript e SQL.

<figure markdown>
  ![Datahub](../../imgs/Datahub.png)
  <figcaption>Datahub</figcaption>
</figure>

[^1]: [Frictionless Data](https://frictionlessdata.io/)

Un [esempio](https://datahub.io/core/co2-ppm) di un set di dati CSV disponibile sulla piattaforma è quello che mostra l'andamento dell'anidride carbonica nell'atmosfera, proveniente dall'Earth System Research Laboratory del governo statunitense.

<figure markdown>
  ![Datahub](../../imgs/Datahub2.png)
  <figcaption>Datahub</figcaption>
</figure>

<figure markdown>
  ![Datahub](../../imgs/Datahub3.png)
  <figcaption>Datahub</figcaption>
</figure>



Il file CSV scaricabile del dataset "CO2 PPM - Trends in Atmospheric Carbon Dioxide" ha le seguenti caratteristiche:
• Dizionario di dati elaborabile in formato JSON secondo la specifica Data Package.
• Riga di intestazione singola.
• Singolo record per riga.
• Denominazione comprensibile delle colonne.
• Struttura dati verticale.
• Trattamento dei valori sconosciuti, indicati da valori di tipo -99,99 (per l'attributo 'media') e -1 (per l'attributo 'giorni').
• Non contiene alcun totale o
raggruppamenti.
• Corretta digitazione dei campi.
• Campo data codificato secondo lo standard ISO- 8601.
• Non contiene dati con coordinate geografiche o campi codificati.

## Kaggle

<figure markdown>
  ![Kaggle](../../imgs/Kaggle.png)
  <figcaption>Kaggle</figcaption>
</figure>