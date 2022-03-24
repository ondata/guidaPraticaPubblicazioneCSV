---
hide:
 - toc
# - navigation
---

È bene riferirsi a schemi standard, *liste di codici* e tassonomie di termini per valori prestabiliti  e codificati di attributi.

Da prendere in considerazione:

  - i codici sono molto utili per eseguire analisi di dati categorizzati, ad esempio per estrarre modelli, filtrare, riassumere e ordinare, ma possono essere difficili da interpretare per le persone che non hanno familiarità con tali codifiche, se non sono spiegate con precisione nel *dataset* stesso o attraverso il [dizionario dei dati](../Dizionario_dati.md);
  - l'[allegato I di questa guida](./Tassonomie_elenchi_codici.md) fornisce una panoramica dei termini riutilizzabili, comprese le tassonomie, le classificazioni e gli standard nazionali e internazionali armonizzati; --->
  - se possibile, si dovrebbe aggiungere una colonna che includa il valore standard dell'attributo in questione; per esempio, se il campo si riferisce ai **comuni**, è consigliabile mantenere due colonne: **"codice_comune"** e **"comune"**; il codice sarà ad esempio per l'Italia il [codice IPA](https://www.indicepa.gov.it/)[^1] del comune e il valore della colonna "comune" sarà invece il nome di tale ente;
  - in linea con quanto detto in precedenza, il nome del campo non dovrebbe essere incluso nel valore dello stesso, per esempio se il nome della colonna è "comune" il valore in ogni riga non dovrebbe includere le parole "Comune di".

[^1]: Indice della Pubblica Amministrazione

### Esempio: uso di campi codificati

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
