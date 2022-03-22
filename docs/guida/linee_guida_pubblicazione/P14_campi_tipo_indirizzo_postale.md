---
hide:
- toc
# - navigation
title: Campi con indirizzi postali
---

# Campi con indirizzi postali

Utilizzare una **codifica accurata degli indirizzi postali** è essenziale per **gestire le dimensioni geografiche con i dati**. Indirizzi postali ben strutturati **possono essere geolocalizzati**, generando coordinate di latitudine e longitudine attraverso l'uso di applicazioni specifiche.

In **Italia** esiste una **regola tecnica** con le specifiche per la modellazione dei dati relativi all'**anagrafe nazionale dei numeri civici e delle strade urbane** definita da AgID[^1] , semplificando al massimo le definizioni previste possiamo raccomandare la definizione degli indirizzi attraverso i seguenti campi:

- **denominazione urbanistica generica** (DUG) come `campo di testo`;
- **denominazione** come come `campo di testo`;
- **civico** come come `campo numerico`;
- **esponente** come come `campo di testo`;
- **città** come come `campo di testo`;
- **codice di avviamento postale** (CAP) come `campo numerico`.

### Esempio 1:
definizione dell'indirizzo attraverso campi specifici.

!!! failure "Cattiva prassi"

    | marchio | indirizzo_rivenditore |
    | --- | --- |
    | chevrolet chevelle malibu | Viale Mazzini n° 5A, Milano (20121) |
    | buick skylark 320 | Località Fabbre 33, 20151 Brera |

!!! success "Buona prassi"

   | marchio | rivenditore_indirizzo_dug | rivenditore_indirizzo_denominazione | rivenditore_indirizzo_civico | rivenditore_indirizzo_esponente | rivenditore_indirizzo_citta | rivenditore_indirizzo_cap |
   | --- | --- | --- | --- | --- | --- | --- |
   | chevrolet chevelle malibu | Viale | Giuseppe Mazzini | 5 | A | Milano | 20100|
   | buick skylark 320 | Località | Fabbre | 33 | `NULL` | Brera | 20151 |

Nel caso precedente per evidenziare che il civico non ha esponente e quindi il campo è stato lasciato intenzionalmente vuoto e per evidenziarlo abbiamo inserito il termine `NULL`, in un caso reale nulla sarebbe stato visualizzato.

**ATTENZIONE DEFINIZIONI IN CONTRASTO CON QUANTO DESCRITTO NEL CAPITOLO SUI VALORI NULL**


Nel caso sia possibile o necessaria la **georeferenziazione degli indirizzi**, ad esempio per una visualizzazione in mappa, è consigliabile **aggiungere due campi** separati per i valori di **latitudine** e **longitudine** corrispondenti al punto geografico dell'indirizzo postale, come suggerito nel capitolo [campi con coordinate geografiche](../P15_campi_con_coordinate_geografiche.md).

[^1]: [Linee guida AgID](https://geodati.gov.it/geoportale/datiterritoriali/regole-tecniche) per la modellazione dei dati relativi all'anagrafe nazionale dei numeri civici e delle strade urbane.

### Esempio 2:
definizione dell'indirizzo attraverso campi specifici e attraverso le coordinate geografiche.

| marchio | rivenditore_indirizzo_dug | rivenditore_indirizzo_denominazione | rivenditore_indirizzo_civico | rivenditore_indirizzo_esponente | rivenditore_indirizzo_citta | rivenditore_indirizzo_cap | latitudine | longitudine |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| chevrolet chevelle malibu | via | Giuseppe Mazzini | 5 | A | Milano | 20100| 44.115684 | 11.123456 |