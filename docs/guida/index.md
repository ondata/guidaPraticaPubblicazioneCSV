---
hide:
 - toc
# - navigation
title: Introduzione
---

# Introduzione

Oggi abbiamo sempre più fonti di dati a portata di mano. Paradossalmente, però, anche se i dati sono più accessibili che mai, le possibilità di riutilizzarli sono piuttosto limitate. I potenziali utenti di questi dati spesso affrontano molteplici barriere all'accesso e all'uso: bassa qualità dei dati, metadati poco descrittivi e standardizzati, licenze imprecise o formati inappropriati.

Queste difficoltà nel riutilizzare i dati sono menzionate in studi di riferimento come l'[Open Data Barometer](https://blog.okfn.org/files/2017/06/FinalreportTheStateofOpenGovernmentDatain2017.pdf), e sono in gran parte dovute alla convinzione iniziale dei produttori di dati che l'importante era pubblicare più informazioni possibili il più presto possibile, indipendentemente dalla loro qualità.

Di conseguenza, i cataloghi di dati pubblicano decine di migliaia di set di dati con carenze di qualità che possono essere identificate solo dopo aver iniziato il processo di riutilizzo, generando un carico di pulizia e preparazione che in molti casi è insostenibile per l'utente. Questo produce frustrazione e perdita di interesse nel settore del riutilizzo, colpendo la credibilità delle istituzioni editoriali e abbassando notevolmente le aspettative di ritorno e generazione di valore dal riutilizzo dei dati aperti.

Per tutte queste ragioni, e tenendo conto dell'attuale stato di maturità delle iniziative sui dati aperti, è il momento di rafforzare il miglioramento della qualità dei dati che vengono pubblicati. Questa guida aiuta chi pubblica dati a usare bene il formato CSV, il più diffuso nella pubblicazione di dati aperti.

## Perché il CSV

- La forma tabellare dei dati è la forma più comune di trasferimento e scambio di informazioni e viene prodotta in diversi modi: file di dati con colonne delimitate o campi di lunghezza fissa, fogli di calcolo, tabelle HTML o download di tabelle di dati SQL, tra gli altri.

- Su [dati.gov.it](https://www.dati.gov.it/), il portale nazionale, oltre 45 mila dataset su circa 74 mila hanno una risorsa in CSV: è il formato più presente (novembre 2026).

- Sul [portale europeo](https://data.europa.eu/) sono quasi 300 mila: più numerosi sono solo i servizi di mappa WMS e WFS (novembre 2026).

- È conciso, facile da interpretare sia per le persone sia per le macchine e adatto alla struttura naturale della maggior parte dei dati. I dati sono disposti in forma di tabella, con i campi separati da un carattere separatore e i record da interruzioni di riga.

- Nessun software specifico è richiesto per aprire i file CSV, basta usare qualsiasi editor di testo disponibile su tutti i sistemi operativi.

## Ma...

- La semplicità di CSV ha il compromesso che il formato non include alcun meccanismo per indicare che tipo di dati sono in una colonna o se i valori in una colonna devono essere espressi in modo obbligatorio. È quindi incline a errori come quelli dei valori mancanti o la mescolanza di diversi tipi di dati all'interno di una colonna.
- La soluzione a questi problemi risiede nell'applicazione di buone pratiche nella fase di preparazione del dataset, nell'articolazione delle misure di controllo della qualità e nel collegamento del file di dati tabulari con schemi che esprimono il modello dei dati attraverso i metadati.



