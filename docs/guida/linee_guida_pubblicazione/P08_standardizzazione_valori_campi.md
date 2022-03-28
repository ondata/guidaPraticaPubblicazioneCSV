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
standardizzazione del nome e del codice dell'attività economica.

!!! failure "Cattiva prassi"

    | marca | attivita_vendite |
    | --- | --- |
    | chevrolet | Vendite di auto |
    | buick | Vendita di veicoli |
    | plymouth | Vendita |

!!! success "Buona prassi"

    | marca | codice_venditore | attivita_vendite |
    | --- | --- | --- |
    | chevrolet | 45.11 | Vendita di automobili e veicoli a motore leggeri |
    | buick | 45.11 | Vendita di automobili e veicoli a motore leggeri |
    | plymouth | 45.19 | Vendita di altri veicoli a motore |



In questo esempio, i valori del campo `codice_venditore` sono quelli corrispondenti alla [classificazione statistica EUROSTAT delle attività economiche della Comunità Europea](https://ec.europa.eu/eurostat/ramon/nomenclatures/index.cfm?TargetUrl=LST_NOM_DTL&StrNom=NACE_REV2&StrLanguageCode=ES&IntPcKey=&StrLayoutCode=HIERARCHIC&IntCurrentPage=1)[^2] per la standardizzazione delle attività economiche dei concessionari di veicoli.

[^2]: NACE Rev. 2
