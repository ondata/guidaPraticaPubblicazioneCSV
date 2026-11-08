---
hide:
 - toc
# - navigation
title: Prima di pubblicare i dati personali
---

# Prima di pubblicare i dati personali

Un numero di telefono, un indirizzo o un codice fiscale in un CSV possono essere dati personali. Questa guida spiega come scriverli, non se puoi pubblicarli: prima di pubblicare, controlla che cosa contiene il file. In una pubblica amministrazione la valutazione del caso concreto spetta a chi ne è responsabile, con il Responsabile della protezione dei dati (RPD).

## Cosa dicono le norme

- **Un dato da pubblicare non è per questo un dato aperto.** I dati personali pubblicati online da una PA su base normativa non sono automaticamente dati di tipo aperto, liberamente riutilizzabili per qualsiasi finalità ([Linee guida AgID](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#sec-requisiti-comuni)).
- **La regola dell'«aperto per default» non vale per i dati personali.** I dati pubblicati senza licenza si intendono aperti, «ad eccezione dei casi in cui la pubblicazione riguardi dati personali» ([Codice dell'amministrazione digitale (CAD), art. 52, comma 2](https://www.normattiva.it/uri-res/N2Ls?urn:nir:stato:decreto.legislativo:2005-03-07;82~art52!vig=)).
- **Anche quando la pubblicazione è prevista, si toglie ciò che non serve.** Le amministrazioni rendono non intelligibili i dati personali non pertinenti alla finalità di trasparenza ([d.lgs. 33/2013, art. 7-bis, comma 4](https://www.normattiva.it/uri-res/N2Ls?urn:nir:stato:decreto.legislativo:2013-03-14;33~art7bis!vig=)).
- **Se il dettaglio espone le persone, si anonimizza prima.** Quando i dati disaggregati violerebbero le norme sulla protezione dei dati, le [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#sec-requisiti-comuni) chiedono procedure di anonimizzazione. Togliere il nome può non bastare.

## Cosa guardare nel file

Sono esempi, non un elenco completo:

- **Telefoni e indirizzi:** quelli di una sede pubblica di norma non pongono problemi, quelli di un privato sì.
- **Codice fiscale:** quello di un ente è un dato pubblico, quello di una persona è un dato personale.
- **Documenti di identità:** numeri e tipi di documento non vanno in un file aperto.
- **Conteggi piccoli:** una riga con un solo caso in un piccolo comune può far riconoscere una persona.
- **Testo libero:** note e descrizioni possono contenere nomi anche quando le altre colonne non ne hanno.
