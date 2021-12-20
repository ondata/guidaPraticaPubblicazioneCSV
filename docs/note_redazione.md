---
hide:
# - toc
 - navigation
title: Note sulla guida
---

# Note sulla guida

A seguire alcune note utili ai redattori della guida

## Modalità di pubblicazione

La guida è basata su [MkDocs](https://www.mkdocs.org/) e sul tema [Material](https://squidfunk.github.io/mkdocs-material/).

## Stile

- creare - ove possibile - i **link ipertestuali** tra i **capitoli**. Quindi ad esempio aggiungere tutti gli *hyperlink* all'indice di [questa pagina](guida/index.md), o laddove si legge qualcosa come "questa possibilità deve essere spiegata nel dizionario", inserire hyperlink al [capitolo sul dizionario](guida/dizionario_dati.md);

## File originali della guida

La cartella [risorse](https://github.com/ondata/guidaPraticaPubblicazioneCSV/tree/main/risorse) del *repository* contiene i file "ufficiali" della guida.

## Foglio con le tabelle di esempio della guida originale

È stato creato un :material-table: [foglio elettronico](https://docs.google.com/spreadsheets/d/1CAR685UYBmaKVB3zE4yuRj-n0fZBL6HohFDat66Zqic/edit#gid=775453510), dove raccogliere senza alcuna formattazione, le tabelle presenti nella guida originale. Sarà comodo per produrre la versione "italiana" da inserire in questa guida.

!!! note "Note per i nomi dei fogli"

    I numeri pagina e la numerazione tabella sempre in doppia cifra (quindi pagina, diventa `01`) e se c'è una sola tabella nella pagina si mantiene lo `01`.<br>
    Come numero pagina, usare quello che si legge nel piede del PDF.

Se per qualche ragione è utile avere anche un `CSV` delle tabelle, inserirle qui nel repo: [docs/risorse/tabelle](https://github.com/ondata/guidaPraticaPubblicazioneCSV/tree/main/docs/risorse/tabelle).

## Come creare tabelle HTML

Nella guida originale in PDF sono presenti tabelle come quella sottostante:

![](imgs/tabella.png)

Non è possibile riprodurla con una tabella in markdown, ma è necessario usare l'HTML. Qui una [guida audio-video](https://www.youtube.com/watch?v=j1jrFGaQh9c), sul come farlo:

<iframe width="560" height="315" src="https://www.youtube.com/embed/j1jrFGaQh9c" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Il *tool online* usato nel video di sopra, per trasformare la tabella di un foglio elettronico in `HTML` è [TableCleaner](https://www.r2h.nl/html-word-excel-table-code-cleaner/index.php).

