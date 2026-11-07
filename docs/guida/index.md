---
hide:
 - toc
# - navigation
title: Perché questa guida
---

# Perché questa guida

Molti dati pubblicati si rivelano difficili da usare solo quando li si apre: colonne spostate, totali mescolati ai dettagli, date scritte in tre modi. Chi li riusa deve prima ripulirli, e a volte rinuncia. Il problema non riguarda il contenuto ma il modo in cui il file è stato preparato, e si può prevenire con poche regole.

Questa guida è per chi in un ente ha i dati in un foglio di calcolo o in un gestionale, deve pubblicarli e non programma. Spiega [cos'è un CSV](formato_dati_tabellari.md), dà [15 regole](linee_guida_pubblicazione/index.md) per prepararlo e dice come [esportarlo da Excel o LibreOffice](linee_guida_pubblicazione/Linee_guida_importazione_esportazione.md).

## Perché il CSV

- La tabella è la forma più comune per scambiare dati, e si ottiene in molti modi: fogli di calcolo, esportazioni da gestionali e database, tabelle HTML.

- Su [dati.gov.it](https://www.dati.gov.it/), il portale nazionale, oltre 45 mila dataset su circa 74 mila hanno una risorsa in CSV: è il formato più presente (novembre 2026).

- Sul [portale europeo](https://data.europa.eu/) sono quasi 300 mila: più numerosi sono solo i servizi di mappa WMS e WFS (novembre 2026).

- È conciso e si lascia leggere sia dalle persone sia dai programmi. I dati sono disposti in tabella: i valori sono separati da un carattere, le righe da un'interruzione di riga.

- Per aprirlo non serve un programma specifico: basta un editor di testo, disponibile su tutti i sistemi operativi.

## Il suo limite

Un CSV non dice se una colonna contiene numeri o testo, né se un valore è obbligatorio. Per questo è facile che ci finiscano valori mancanti o tipi mescolati.

Il rimedio sta in tre cose: preparare bene il file ([le regole](linee_guida_pubblicazione/index.md)), controllarlo ([gli strumenti](linee_guida_pubblicazione/Cassetta_attrezzi.md)) e accompagnarlo con una descrizione delle colonne ([il dizionario dei dati](dizionario_dati.md)).

## Cosa copre la guida

Le regole e gli strumenti di questa guida riguardano la forma del file: struttura, tipi, coerenza interna. Non dicono se i valori sono giusti: un file senza errori di formato può contenere un numero di prestiti sbagliato.

Le Linee guida AgID distinguono sei [livelli di validazione](https://ondata.github.io/linee-guida-opendata/capitolo-5.html#sec-validazione), dalla coerenza con i requisiti strutturali al confronto con i dati di altri fornitori: i controlli descritti qui si fermano, in sostanza, ai primi due, cioè alla struttura e alla coerenza all'interno del dataset. Controllare il file non basta: AgID raccomanda di garantire almeno accuratezza, coerenza, completezza e attualità dei dati ([raccomandazione 8](https://ondata.github.io/linee-guida-opendata/capitolo-5.html#racc-8)).

Nel [modello a 5 stelle](https://ondata.github.io/linee-guida-opendata/allegato-A.html) il CSV arriva a 3 stelle, il livello minimo richiesto dalle Linee guida AgID. La quarta richiede RDF, un modo di descrivere i dati collegandoli fra loro, e SPARQL, il linguaggio per interrogarli. [Valori uniformi](linee_guida_pubblicazione/P08_standardizzazione_valori_campi.md) e [codici standard](linee_guida_pubblicazione/P09_campi_codificati.md) non fanno salire di stella, ma preparano quel passaggio.

## La guida e le norme

Questa guida è una buona pratica volontaria, non un atto normativo. Il CSV non è obbligatorio in sé: è un modo per rispettare gli obblighi qui sotto. Ultimo controllo dei riferimenti: 7 novembre 2026.

**Obblighi di legge.** Ogni norma ha i propri destinatari: controlla quali si applicano al tuo ente.

- i dati oggetto di pubblicazione obbligatoria vanno in formato di tipo aperto ([d.lgs. 33/2013, art. 7](https://www.normattiva.it/uri-res/N2Ls?urn:nir:stato:decreto.legislativo:2013-03-14;33~art7!vig=));
- i dati pubblicati senza licenza si intendono aperti, salvo i dati personali ([Codice dell'amministrazione digitale (CAD), art. 52, comma 2](https://www.normattiva.it/uri-res/N2Ls?urn:nir:stato:decreto.legislativo:2005-03-07;82~art52!vig=));
- un formato aperto è documentato e neutro rispetto agli strumenti, e i dati di tipo aperto sono anche adatti all'uso automatico e provvisti di metadati ([CAD, art. 1, comma 1, lettere l-bis e l-ter](https://www.normattiva.it/uri-res/N2Ls?urn:nir:stato:decreto.legislativo:2005-03-07;82~art1!vig=));
- ogni anno si pubblicano sul sito dell'ente gli elenchi delle categorie di dati detenuti ([d.lgs. 36/2006, art. 9](https://www.normattiva.it/uri-res/N2Ls?urn:nir:stato:decreto.legislativo:2006-01-24;36~art9!vig=)).

**Regole tecniche**, nelle [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/) (determinazione 183/2023):

- formato aperto e leggibile meccanicamente, di almeno 3 stelle: il CSV le raggiunge ([requisito 2](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-2));
- metadati conformi al profilo italiano (DCAT-AP_IT) o, per i dati territoriali, alle Linee guida del Repertorio nazionale dei dati territoriali (RNDT) ([requisiti 15](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-15) e [16](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-16)), da inserire e tenere aggiornati su dati.gov.it o nel RNDT ([requisiti 29](https://ondata.github.io/linee-guida-opendata/capitolo-7.html#req-29) e [30](https://ondata.github.io/linee-guida-opendata/capitolo-7.html#req-30));
- licenza CC BY per i nuovi dati aperti nativi, cioè prodotti dalle amministrazioni; una licenza diversa da CC BY 4.0 o CC0 va motivata formalmente ([requisiti 20](https://ondata.github.io/linee-guida-opendata/capitolo-6.html#req-20) e [21](https://ondata.github.io/linee-guida-opendata/capitolo-6.html#req-21)).

**Buona pratica:** le regole di questa guida, che dettagliano ciò che le norme lasciano aperto. Dove riprendono l'[Allegato B delle Linee guida AgID](https://ondata.github.io/linee-guida-opendata/allegato-B.html#csv), sono indicazioni e non requisiti.

**Quando il CSV non basta.** I dati dinamici e le serie di dati di elevato valore vanno resi disponibili anche attraverso API, interfacce con cui un programma interroga i dati ([requisiti 5](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-5) e [7](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-7); [Regolamento di esecuzione (UE) 2023/138](https://eur-lex.europa.eu/legal-content/IT/TXT/HTML/?uri=CELEX:32023R0138)). Il CSV resta utile per lo scaricamento in blocco.

## Come adottarla in un ente

Quella che segue è una proposta, non una procedura prevista da una norma.

Le Linee guida AgID raccomandano di affidare al Responsabile per la transizione digitale (RTD) un gruppo di lavoro sull'apertura dei dati ([raccomandazione 4](https://ondata.github.io/linee-guida-opendata/capitolo-5.html#racc-4)): quel gruppo può adottare questa guida come riferimento interno, citandone una versione precisa, con numero e DOI, come spiegato in [Partecipa](../partecipa.md).

La guida può entrare anche nei contratti. Il CAD chiede di prevedere nei capitolati che riguardano formazione, raccolta e gestione di dati clausole che ne consentano l'utilizzazione ([art. 52, comma 3](https://www.normattiva.it/uri-res/N2Ls?urn:nir:stato:decreto.legislativo:2005-03-07;82~art52!vig=)). Le Linee guida AgID raccomandano un approccio «open by design» fin dalla progettazione, con clausole contrattuali sulla proprietà del dataset e sulla sua fruibilità nel tempo, compreso l'uso di formati aperti ([par. 6.1.2](https://ondata.github.io/linee-guida-opendata/capitolo-6.html#sec-buone-pratiche-approccio-open-by-design)).

!!! note "Bozza di clausola, da adattare e da far rivedere a chi scrive i capitolati"

    I dati tabellari prodotti nell'ambito del contratto sono consegnati in formato CSV secondo la RFC 4180 e le raccomandazioni dell'Allegato B delle Linee guida AgID (determinazione 183/2023), secondo le 15 regole della «Guida pratica alla pubblicazione di dati in CSV», versione [numero], e corredati di dizionario dei dati.
