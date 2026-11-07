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

## La guida e le norme

Questa guida è una buona pratica volontaria, non un atto normativo. Il CSV non è obbligatorio in sé: è un modo per rispettare gli obblighi qui sotto. Ultimo controllo dei riferimenti: 7 novembre 2026.

**Obblighi di legge.** Ogni norma ha i propri destinatari: controlla quali si applicano al tuo ente.

- i dati oggetto di pubblicazione obbligatoria vanno in formato di tipo aperto ([d.lgs. 33/2013, art. 7](https://www.normattiva.it/uri-res/N2Ls?urn:nir:stato:decreto.legislativo:2013-03-14;33~art7!vig=));
- i dati pubblicati senza licenza si intendono aperti, salvo i dati personali ([CAD, art. 52, comma 2](https://www.normattiva.it/uri-res/N2Ls?urn:nir:stato:decreto.legislativo:2005-03-07;82~art52!vig=));
- un formato aperto è documentato e neutro rispetto agli strumenti, e i dati di tipo aperto sono anche adatti all'uso automatico e provvisti di metadati ([CAD, art. 1, comma 1, lettere l-bis e l-ter](https://www.normattiva.it/uri-res/N2Ls?urn:nir:stato:decreto.legislativo:2005-03-07;82~art1!vig=));
- ogni anno si pubblicano sul sito dell'ente gli elenchi delle categorie di dati detenuti ([d.lgs. 36/2006, art. 9](https://www.normattiva.it/uri-res/N2Ls?urn:nir:stato:decreto.legislativo:2006-01-24;36~art9!vig=)).

**Regole tecniche**, nelle [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/) (determinazione 183/2023):

- formato aperto e leggibile meccanicamente, di almeno 3 stelle: il CSV le raggiunge ([requisito 2](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-2));
- metadati conformi a DCAT-AP_IT o, per i dati territoriali, alle Linee guida RNDT ([requisiti 15](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-15) e [16](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-16)), da inserire e tenere aggiornati su dati.gov.it o nel RNDT ([requisiti 29](https://ondata.github.io/linee-guida-opendata/capitolo-7.html#req-29) e [30](https://ondata.github.io/linee-guida-opendata/capitolo-7.html#req-30));
- licenza CC BY per i nuovi dati aperti nativi; una licenza diversa da CC BY 4.0 o CC0 va motivata formalmente ([requisiti 20](https://ondata.github.io/linee-guida-opendata/capitolo-6.html#req-20) e [21](https://ondata.github.io/linee-guida-opendata/capitolo-6.html#req-21)).

**Buona pratica:** le regole di questa guida, che dettagliano ciò che le norme lasciano aperto. Dove riprendono l'[Allegato B delle Linee guida AgID](https://ondata.github.io/linee-guida-opendata/allegato-B.html#csv), sono indicazioni e non requisiti.

**Quando il CSV non basta.** I dati dinamici e le serie di dati di elevato valore vanno resi disponibili anche attraverso API ([requisiti 5](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-5) e [7](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-7); [Regolamento di esecuzione (UE) 2023/138](https://eur-lex.europa.eu/legal-content/IT/TXT/HTML/?uri=CELEX:32023R0138)). Il CSV resta utile per lo scaricamento in blocco.
