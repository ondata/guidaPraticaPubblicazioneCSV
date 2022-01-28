---
hide:
 - toc
# - navigation
---

È bene riferirsi a schemi standard, a *liste di codici* e tassonomie di termini, per valori prestabiliti  e codificati di attributi.

Da prendere in considerazione:

  - Sono molto utili per eseguire analisi di dati categorizzati (ad esempio per estrarre modelli, filtrare, riassumere, ordinare, ecc.), ma possono essere difficili da interpretare per le persone che non hanno familiarità con tali codifiche, se non sono spiegate con precisione nel *dataset* stesso o attraverso il [Dizionario dei Dati](../dizionario_dati.md).
  - L'allegato I di questa guida (⚠️ **ancora da scrivere**) fornisce una panoramica dei termini riutilizzabili, comprese le tassonomie, le classificazioni e gli standard nazionali e internazionali armonizzati.
  - Se possibile, si dovrebbe aggiungere una colonna che includa il valore standard dell'attributo in questione. Per esempio, se il campo si riferisce ai Comuni, è consigliabile mantenere due colonne: "Codice Comune" e "Comune". Il Codice sarà ad esempio (per l'Italia) il [codice IPA](https://www.indicepa.gov.it/) (Indice della Pubblica Amministrazione) del Comune, e il valore della colonna "Comune" sarà invece il nome di tale ente.
  - In linea con quanto detto in precedenza, il nome del campo non dovrebbe essere incluso nel valore dello stesso. Per esempio, se il nome della colonna è "Comune" il valore in ogni riga non dovrebbe includere le parole "Comune di".

**Esempio**: uso di campi codificati

!!! failure "Cattiva prassi"


    | marca | consumo | potenza | cambio | accelerazione |
    | --- | ---: | ---: | --- | ---: |
    | chevrolet chevelle malibu | 18 | 130 | M | 12 |
    | buick skylark 320 | 15 | 165 | A | 11.5 |
    | plymouth satellite | 18 | 150 | A | 11 |
    | amc rebel sst | 16 | 150 | M | 12 |
    | ford torino | 17 | 140 | M | 10.5 |

!!! success "Buona prassi"

    | marca | consumo | potenza | cambio | cambio_descrizione | accelerazione |
    | --- | ---: | ---: | --- | --- | ---: |
    | chevrolet chevelle malibu | 18 | 130 | M | Manuale | 12 |
    | buick skylark 320 | 15 | 165 | A | Automatico | 11.5 |
    | plymouth satellite | 18 | 150 | A | Automatico | 11 |
    | amc rebel sst | 16 | 150 | M | Manuale | 12 |
    | ford torino | 17 | 140 | M | Manuale | 10.5 |
