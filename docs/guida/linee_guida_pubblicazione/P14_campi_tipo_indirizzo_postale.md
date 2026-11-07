---
hide:
- toc
# - navigation
title: Dividi gli indirizzi in colonne
---

# 14. Dividi gli indirizzi in colonne

Meglio dividere l'indirizzo in più colonne, una per ogni parte (`dug`, `denominazione`, `civico`, `esponente`, `comune`, `cap`), invece di scriverlo tutto in una cella.

## Così sì e così no

Nomi delle biblioteche e indirizzi di questa pagina sono inventati. I nomi dei comuni sono veri.

!!! failure "Così no"

    | biblioteca | indirizzo |
    | --- | --- |
    | Biblioteca di esempio A | Via Roma n° 10, Palermo (90133) |
    | Biblioteca di esempio B | Piazza Cavour 1/B, 10060 None |
    | Biblioteca di esempio C | Via Garibaldi 4 - 26040 Cella Dati |
    | Biblioteca di esempio D | Via Cavour, 20, Roma 00184 |

!!! success "Così sì"

    | biblioteca | dug | denominazione | civico | esponente | comune | cap |
    | --- | --- | --- | ---: | --- | --- | --- |
    | Biblioteca di esempio A | Via | Roma | 10 |  | Palermo | 90133 |
    | Biblioteca di esempio B | Piazza | Cavour | 1 | B | None | 10060 |
    | Biblioteca di esempio C | Via | Garibaldi | 4 |  | Cella Dati | 26040 |
    | Biblioteca di esempio D | Via | Cavour | 20 |  | Roma | 00184 |

Aperte con un editor di testo, le stesse righe si leggono così. Lo zero iniziale di `00184` deve restare:

```csv
biblioteca,dug,denominazione,civico,esponente,comune,cap
Biblioteca di esempio A,Via,Roma,10,,Palermo,90133
Biblioteca di esempio B,Piazza,Cavour,1,B,None,10060
Biblioteca di esempio C,Via,Garibaldi,4,,Cella Dati,26040
Biblioteca di esempio D,Via,Cavour,20,,Roma,00184
```

## Perché

Con le parti separate, chi riusa i dati può filtrare per comune o per CAP, incrociare gli indirizzi con ANNCSU e geolocalizzarli, cioè ricavarne latitudine e longitudine con programmi specifici. Da `Via Roma n° 10, Palermo (90133)` un programma deve indovinare dove finisce la strada e dove comincia il comune.

Il CAP è un codice, non un numero: letto come numero, `00184` diventa `184`.

## Casi particolari

### Le colonne e ANNCSU

In Italia il riferimento nazionale per strade e numeri civici è l'[Archivio nazionale dei numeri civici e delle strade urbane](https://www.anncsu.gov.it/it/) (ANNCSU), gestito da Istat e Agenzia delle Entrate con i dati certificati dai Comuni, e pubblicato anche in [CSV aperti](https://www.anncsu.gov.it/it/consultazione-dellarchivio/open-data/) aggiornati ogni mese[^1]. In forma semplificata, consigliamo queste colonne:

- **dug**: denominazione urbanistica generica (`Via`, `Piazza`), testo;
- **denominazione**: il nome della strada, testo;
- **civico**: numero;
- **esponente**: testo, in una colonna a sé (`B`);
- **comune**: testo;
- **cap**: codice di avviamento postale, testo di 5 caratteri.

Se puoi, aggiungi il progressivo nazionale del civico e il codice Istat del comune: permettono di incrociare il dato con l'archivio.

### Coordinate

Se serve la mappa, meglio aggiungere due colonne con latitudine e longitudine del punto, come spiega la scheda sulle [coordinate geografiche](P15_campi_con_coordinate_geografiche.md):

| biblioteca | dug | denominazione | civico | esponente | comune | cap | latitudine | longitudine |
| --- | --- | --- | ---: | --- | --- | --- | ---: | ---: |
| Biblioteca di esempio A | Via | Roma | 10 |  | Palermo | 90133 | 38.1157 | 13.3615 |
| Biblioteca di esempio D | Via | Cavour | 20 |  | Roma | 00184 | 41.8950 | 12.4950 |

### Dati personali

L'indirizzo di un privato è un dato personale: vedi [Prima di pubblicare i dati personali](Dati_personali.md).

## Come si fa nel foglio di calcolo

Prima di esportare, usa il formato Testo per `cap` e per il codice Istat del comune. Poi apri il file con un editor di testo e controlla che gli zeri iniziali ci siano ancora. La procedura è nella pagina su [Excel e LibreOffice](Linee_guida_importazione_esportazione.md).

[^1]: Gli indirizzi fanno parte dei dati di elevato valore del Regolamento di esecuzione (UE) 2023/138. Le specifiche sono di [Istat e Agenzia delle Entrate](https://www.istat.it/wp-content/uploads/2022/05/Specifiche-tecniche-anccsu-2024.pdf); per la modellazione vedi le [regole tecniche sui dati territoriali](https://geodati.gov.it/geoportale/datiterritoriali/regole-tecniche).

Vedi anche: [9. Affianca una descrizione ai codici](P09_campi_codificati.md), [15. Scrivi le coordinate in gradi decimali](P15_campi_con_coordinate_geografiche.md).
