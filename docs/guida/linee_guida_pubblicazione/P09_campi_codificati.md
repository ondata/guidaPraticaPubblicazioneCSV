---
hide:
 - toc
# - navigation
---

È bene riferirsi a schemi standard, *liste di codici* e tassonomie di termini per valori prestabiliti e codificati di attributi.

Da prendere in considerazione:

  - un codice fatto di cifre è un testo, non un numero: non ci si fanno operazioni e gli zeri iniziali contano. Vale per codici Istat, CAP, codici fiscali e di attività. Dichiaralo come testo nel dizionario e controlla che gli zeri siano ancora lì prima di pubblicare, aprendo il file con un editor di testo;
  - i codici sono molto utili per eseguire analisi di dati categorizzati, ad esempio per estrarre modelli, filtrare, riassumere e ordinare, ma possono essere difficili da interpretare per le persone che non hanno familiarità con tali codifiche, se non sono spiegate con precisione nel *dataset* stesso o attraverso il [dizionario dei dati](../dizionario_dati.md);
  - la pagina [Tassonomie ed elenchi di codici](./Tassonomie_elenchi_codici.md) raccoglie classificazioni e standard riutilizzabili;
  - se possibile, si dovrebbe aggiungere una colonna che includa il valore standard dell'attributo in questione; per esempio, se il campo si riferisce ai **comuni**, è consigliabile mantenere due colonne: **"codice_comune"** e **"comune"**; il codice sarà, per l'Italia, il codice Istat del comune, di 6 caratteri ([SITUAS](https://situas.istat.it/web/)), e il valore della colonna "comune" sarà il suo nome. Se la colonna indica invece l'amministrazione che ha prodotto il dato o che eroga un servizio, il riferimento è il [codice IPA](https://www.indicepa.gov.it/ipa-portale/)[^1];
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
