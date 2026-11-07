---
hide:
- toc
# - navigation
title: Campi con indirizzi postali
---

# Campi con indirizzi postali

L'indirizzo di un privato è un dato personale: vedi [Prima di pubblicare i dati personali](Dati_personali.md).

Utilizzare una **codifica accurata degli indirizzi postali** è essenziale per **gestire le dimensioni geografiche con i dati**. Indirizzi postali ben strutturati **possono essere geolocalizzati**, generando coordinate di latitudine e longitudine attraverso l'uso di applicazioni specifiche.

In **Italia** il riferimento nazionale per strade e numeri civici è l'[Archivio nazionale dei numeri civici e delle strade urbane](https://www.anncsu.gov.it/it/) (ANNCSU), gestito da Istat e Agenzia delle Entrate con i dati certificati dai Comuni, e pubblicato anche in [CSV aperti](https://www.anncsu.gov.it/it/consultazione-dellarchivio/open-data/) aggiornati ogni mese[^1]. Se puoi, aggiungi il progressivo nazionale del civico e il codice Istat del comune: permettono di incrociare il dato con l'archivio. In forma semplificata, consigliamo questi campi:

- **denominazione urbanistica generica** (DUG) come `campo di testo`;
- **denominazione** come `campo di testo`;
- **civico** come `campo numerico`;
- **esponente** come `campo di testo`;
- **città** come `campo di testo`;
- **codice di avviamento postale** (CAP) come `campo di testo`, di 5 caratteri.

### Esempio 1:
definizione dell'indirizzo attraverso campi specifici.

!!! failure "Cattiva prassi"

    | marchio | indirizzo_rivenditore |
    | --- | --- |
    | chevrolet chevelle malibu | Viale Mazzini n° 5A, Milano (20121) |
    | buick skylark 320 | Località Fabbre 33, 20151 Brera |

!!! success "Buona prassi"

    | marchio | rivenditore_indirizzo_dug | rivenditore_indirizzo_denominazione | rivenditore_indirizzo_civico | rivenditore_indirizzo_esponente | rivenditore_indirizzo_citta | rivenditore_indirizzo_cap |
    | --- | --- | --- | ---: | --- | --- | --- |
    | chevrolet chevelle malibu | Viale | Giuseppe Mazzini | 5 | A | Milano | 20121 |
    | buick skylark 320 | Località | Fabbre | 33 |  | Milano | 20151 |



Nel caso sia possibile o necessaria la **georeferenziazione degli indirizzi**, ad esempio per una visualizzazione in mappa, è consigliabile **aggiungere due campi** separati per i valori di **latitudine** e **longitudine** corrispondenti al punto geografico dell'indirizzo postale, come suggerito nel capitolo [campi con coordinate geografiche](P15_campi_con_coordinate_geografiche.md).

[^1]: Gli indirizzi fanno parte dei dati di elevato valore del Regolamento di esecuzione (UE) 2023/138. Le specifiche sono di [Istat e Agenzia delle Entrate](https://www.istat.it/wp-content/uploads/2022/05/Specifiche-tecniche-anccsu-2024.pdf); per la modellazione vedi le [regole tecniche sui dati territoriali](https://geodati.gov.it/geoportale/datiterritoriali/regole-tecniche).

### Esempio 2:
definizione dell'indirizzo attraverso campi specifici e attraverso le coordinate geografiche.

| marchio | rivenditore_indirizzo_dug | rivenditore_indirizzo_denominazione | rivenditore_indirizzo_civico | rivenditore_indirizzo_esponente | rivenditore_indirizzo_citta | rivenditore_indirizzo_cap | latitudine | longitudine |
| --- | --- | --- | ---: | --- | --- | --- | ---: | ---: |
| chevrolet chevelle malibu | Viale | Giuseppe Mazzini | 5 | A | Milano | 20121 | 45.47 | 9.19 |
