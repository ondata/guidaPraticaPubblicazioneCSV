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
- la codifica e la standardizzazione utilizzate si basano su alcuni standard comuni proposti e utilizzati da altre organizzazioni nazionali o internazionali come ad eempio [EUROSTAT](https://ec.europa.eu/eurostat/ramon/nomenclatures/index.cfm?TargetUrl=LST_NOM_DTL&StrNom=NACE_REV2&StrLanguageCode=ES&IntPcKey=&StrLayoutCode=HIERARCHIC&IntCurrentPage=1) o [ISTAT](https://www.istat.it/it/metodi-e-strumenti/classificazioni).

Si raccomanda:

- di utilizzare vocabolari comunemente usati, per standardizzare la struttura e i valori delle informazioni pubblicate nei dataset[^1];
- nel caso in cui non si utilizzino vocabolari di riferimento, il valore assegnato ad un dato attributo deve essere unico e coerente in tutta la tabella; in altre parole, se si sceglie di usare il valore "Barcellona" per riferirsi a questa città, non si dovrebbe usare ad esempio il valore "Città di Barcellona".

[^1]: Lo standard AENOR 137801:2015 include un elenco di vocabolari di riferimento: <http://vocab.linkeddata.es/datosabiertos/>


### Esempio:
un caso che si presenta di frequente è quando abbiamo un dato in cui in una colonna compare la dimensione territoriale. Abbiamo ad esempio una colonna "Comune" oppure "Provincia" o "Regione". Spesso ci si limita a valorizzare il campo con la descrizione di quel Comune, quella Provincia o quella Regione, ma  diventa così molto facile utilizzare descrizioni non standard. Ad esempio "Reggio Emilia" al posto di "Reggio nell'Emilia" o "Reggio Calabria" al posto di "Reggio di Calabria". Generando peraltro ulteriore confusione sul fatto che andrebbe specificato se ci si sta riferendo al comune o alla provincia "Reggio di Calabria" .  Per ovviare a questo problema è possibile introdurre nel nostro dataset una nuova colonna con il codice standard Istat di quella provincia o di quel comune.

!!! failure "Cattiva prassi"

    | territorio | popolazione_residente_al_31_dicembre |
    | --- | --- |
    | Reggio nell'Emilia | 524856 |
    | Reggio di Calabria | 523791 |
    | Napoli | 2986745 |

!!! success "Buona prassi"

     | territorio | codice_territorio | popolazione_residente_al_31_dicembre |
    | --- | --- | --- |
    | Reggio nell'Emilia | 35 | 524856 |
    | Reggio di Calabria | 80 | 523791 |
    | Napoli | 63 | 2986745 |

o, nel caso ci si sta riferendo a dati a livello comunale

!!! success "Buona prassi"

     | territorio | codice_territorio | popolazione_residente_al_31_dicembre |
    | --- | --- | --- |
    | Reggio nell'Emilia | 35033 | 170601 |
    | Reggio di Calabria | 80063 | 173026 |
    | Napoli | 63049 | 922094 |


Tutti i dati hanno poi un "tempo" a cui si riferiscono. Poichè il dato sulla popolazione residente è un dato annuale, diventa importante l'inserimento di una colonna che specifichi l'anno di riferimento. La tabella con i dati comunali diventa coì la seguente

!!! success "Buona prassi"

     | territorio | codice_territorio | popolazione_residente_al_31_dicembre | anno |
    | --- | --- | --- | --- |
    | Reggio nell'Emilia | 35033 | 170601 | 2020 |
    | Reggio di Calabria | 80063 | 173026 | 2020 |
    | Napoli | 63049 | 922094 | 2020 |



### Esempio:
un altro esempio lo possiamo avere con la standardizzazione del nome e del codice dell'attività economica. Nell'esempio che segue è stato introdotto nella tabella il codice NACE delle attività economiche così come descritte da EUROSTAT

!!! failure "Cattiva prassi"

    | marca | attivita_vendite |
    | --- | --- |
    | chevrolet | Vendite di auto |
    | buick | Vendita di veicoli |
    | plymouth | Vendita |

!!! success "Buona prassi"

    | marca | codice_venditore | attivita_vendite |
    | --- | ---: | --- |
    | chevrolet | 45.11 | Vendita di automobili e veicoli a motore leggeri |
    | buick | 45.11 | Vendita di automobili e veicoli a motore leggeri |
    | plymouth | 45.19 | Vendita di altri veicoli a motore |



I valori del campo `codice_venditore` sono quelli corrispondenti alla [classificazione statistica EUROSTAT delle attività economiche della Comunità Europea](https://ec.europa.eu/eurostat/ramon/nomenclatures/index.cfm?TargetUrl=LST_NOM_DTL&StrNom=NACE_REV2&StrLanguageCode=ES&IntPcKey=&StrLayoutCode=HIERARCHIC&IntCurrentPage=1)[^2] per la standardizzazione delle attività economiche dei concessionari di veicoli.

[^2]: NACE Rev. 2
