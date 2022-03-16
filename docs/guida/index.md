---
hide:
 - toc
# - navigation
title: Introduzione
---

# Introduzione

Oggi abbiamo sempre più fonti di dati a portata di mano. Paradossalmente, però, anche se i dati sono più accessibili che mai, le possibilità di riutilizzarli sono piuttosto limitate. I potenziali utenti di questi dati spesso affrontano molteplici barriere all'accesso e all'uso: bassa qualità dei dati, metadati poco descrittivi e standardizzati, licenze imprecise o formati inappropriati.

Queste difficoltà nel riutilizzare i dati sono menzionate in diversi studi di riferimento come l'[Open Data Barometer](https://blog.okfn.org/files/2017/06/FinalreportTheStateofOpenGovernmentDatain2017.pdf) o il [Global Open Data](https://index.okfn.org/), e sono in gran parte dovute alla convinzione iniziale dei produttori di dati che l'importante era pubblicare più informazioni possibili il più presto possibile, indipendentemente dalla loro qualità.

Di conseguenza, i cataloghi di dati pubblicano decine di migliaia di set di dati con carenze di qualità che possono essere identificate solo dopo aver iniziato il processo di riutilizzo, generando un carico di pulizia e preparazione che in molti casi è insostenibile per l'utente. Questo produce frustrazione e perdita di interesse nel settore del riutilizzo, colpendo la credibilità delle istituzioni editoriali e abbassando notevolmente le aspettative di ritorno e generazione di valore dal riutilizzo dei dati aperti.

Per tutte queste ragioni, e tenendo conto dell'attuale stato di maturità delle iniziative sui dati aperti, è il momento di rafforzare il miglioramento della qualità dei dati che vengono pubblicati. Questa guida è la prima pubblicazione di un compendio di linee guida compilato con lo scopo di guidare gli editori nell'uso appropriato di formati e mezzi di accesso ai dati aperti. In questa occasione, il focus è sul formato CSV, che è il formato più utilizzato nella pubblicazione di dati aperti.

## Perché il CSV

- La forma tabellare dei dati è la forma più comune di trasferimento e scambio di informazioni e viene prodotta in diversi modi: file di dati con colonne delimitate o campi di lunghezza fissa, fogli di calcolo, tabelle HTML o download di tabelle di dati SQL, tra gli altri.

- Questo è il formato più popolare e ampiamente utilizzato nel contesto del riutilizzo degli Open Data. La maggior parte delle risorse disponibili nei cataloghi Open Data sono in formato CSV.

- Il portale europeo dei dati ha più di 120.000 set di dati [in formato CSV, il](https://www.europeandataportal.eu/data/datasets?locale=es) [formato più abbondante in questo <span class="underline">catalogo Open Data</span>.](https://www.europeandataportal.eu/data/datasets?locale=es)

- Da parte sua, il catalogo nazionale [<span class="underline">datos.gob.es</span>](https://datos.gob.es/en/catalogo) ha quasi 14 mila set di dati in formato CSV, che è anche il formato più comune.

- È conciso, facile da interpretare sia per gli uomini che per le macchine e adatto alla struttura naturale della maggior parte dei dati. È caratterizzato da [<span class="underline">dati disposti in forma di tabella,</span>](https://datos.gob.es/es/documentacion/como-generar-valor-partir-de-los-datos-formatos-tecnicas-y-herramientas-para-analizar%20que%20cataloga%20el%20CSV%20como%20un%20formato%20que%20para%20personas%20y%20para%20m%C3%A1quinas%20\(hibrido\)) dove i campi sono separati da un carattere separatore e i record da interruzioni di riga.

- Nessun software specifico è richiesto per aprire i file CSV, basta usare qualsiasi editor di testo disponibile su tutti i sistemi operativi.

## Ma...

- La semplicità di CSV ha il compromesso che il formato non include alcun meccanismo per indicare che tipo di dati sono in una colonna o se i valori in una colonna devono essere espressi in modo obbligatorio. È quindi incline a errori come quelli dei valori mancanti o la mescolanza di diversi tipi di dati all'interno di una colonna.
- La soluzione a questi problemi risiede nell'applicazione di buone pratiche nella fase di preparazione del dataset, nell'articolazione delle misure di controllo della qualità e nel collegamento del file di dati tabulari con schemi che esprimono il modello dei dati attraverso i metadati.



