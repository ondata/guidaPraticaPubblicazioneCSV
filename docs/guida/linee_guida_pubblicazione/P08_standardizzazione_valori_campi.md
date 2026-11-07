---
hide:
 - toc
# - navigation
title: Standardizzazione del valori dei campi
---

# Standardizzazione del valori dei campi

L'utilizzo di classificazioni, vocabolari e più in generale di metadati "standard" permette di combinare tra loro dati provenienti da fonti differenti, abilitandone in questo modo l'interoperabilità.

Vanno considerati tecnicamente corretti quei dati che:

- usano la stessa codifica e normalizzazione per lo stesso tipo di dati, pubblicati in diversi dataset di un catalogo, per esempio, gli indirizzi sono sempre pubblicati con la stessa struttura, tipo, formato, in qualsiasi dataset e i dati geografici hanno lo stesso sistema di coordinate;
- la codifica e la standardizzazione utilizzate si basano su alcuni standard comuni proposti e utilizzati da altre organizzazioni nazionali o internazionali come ad esempio [EUROSTAT](https://ec.europa.eu/eurostat/web/nace) o [ISTAT](https://www.istat.it/it/metodi-e-strumenti/classificazioni).

Si raccomanda:

- di utilizzare vocabolari comunemente usati, per standardizzare la struttura e i valori delle informazioni pubblicate nei dataset[^1];
- nel caso in cui non si utilizzino vocabolari di riferimento, il valore assegnato ad un dato attributo deve essere unico e coerente in tutta la tabella; in altre parole, se si sceglie di usare il valore "Palermo" per riferirsi a questa città, non si dovrebbe usare ad esempio il valore "Comune di Palermo".

[^1]: Le [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/capitolo-5.html#sec-arricchimento) indicano il Catalogo nazionale della semantica dei dati.


## Esempio 1

Un caso che si presenta di frequente è quando abbiamo un dato in cui in una colonna compare la dimensione territoriale. Abbiamo ad esempio una colonna "Comune" oppure "Provincia" o "Regione". Spesso ci si limita a valorizzare il campo con la descrizione di quel Comune, quella Provincia o quella Regione, ma  diventa così molto facile utilizzare descrizioni non standard. Ad esempio "Reggio Emilia" al posto di "Reggio nell'Emilia" o "Reggio Calabria" al posto di "Reggio di Calabria". Generando peraltro ulteriore confusione sul fatto che andrebbe specificato se ci si sta riferendo al comune o alla provincia "Reggio di Calabria" .  Per ovviare a questo problema è possibile introdurre nel nostro dataset una nuova colonna con il codice standard Istat di quel comune.

!!! failure "Cattiva prassi"

    | territorio | popolazione_residente_al_31_dicembre |
    | --- | --- |
    | Reggio nell'Emilia | 170601 |
    | Reggio di Calabria | 173026 |
    | Napoli | 922094 |

!!! success "Buona prassi"

     | territorio | codice_territorio | popolazione_residente_al_31_dicembre |
    | --- | --- | --- |
    | Reggio nell'Emilia | 035033 | 170601 |
    | Reggio di Calabria | 080063 | 173026 |
    | Napoli | 063049 | 922094 |


Tutti i dati hanno poi un "tempo" a cui si riferiscono. Poichè il dato sulla popolazione residente è un dato annuale, diventa importante l'inserimento di una colonna che specifichi l'anno di riferimento. La tabella con i dati comunali diventa coì la seguente

!!! success "Buona prassi"

     | territorio | codice_territorio | popolazione_residente_al_31_dicembre | anno |
    | --- | --- | --- | --- |
    | Reggio nell'Emilia | 035033 | 170601 | 2020 |
    | Reggio di Calabria | 080063 | 173026 | 2020 |
    | Napoli | 063049 | 922094 | 2020 |



## Esempio 2

Un altro esempio lo possiamo avere con la standardizzazione del nome e del codice dell'attività economica. Nell'esempio che segue è stato introdotto nella tabella il codice Ateco delle attività economiche, nella classificazione di Istat

!!! failure "Cattiva prassi"

    | marca | attivita_vendite |
    | --- | --- |
    | chevrolet | Vendite di auto |
    | buick | Vendita di veicoli |
    | plymouth | Vendita |

!!! success "Buona prassi"

    | marca | codice_ateco_2025 | attivita_vendite |
    | --- | --- | --- |
    | chevrolet | 47.81 | Commercio al dettaglio di autoveicoli |
    | buick | 47.81 | Commercio al dettaglio di autoveicoli |
    | plymouth | 46.71 | Commercio all'ingrosso di autoveicoli |



I valori del campo `codice_ateco_2025` sono quelli della [classificazione Ateco 2025 di Istat](https://www.istat.it/classificazione/ateco-2025/). Le classificazioni hanno versioni: dichiara quella usata, come fa qui il nome della colonna.
