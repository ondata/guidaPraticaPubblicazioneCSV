---
hide:
 - toc
# - navigation
---

# Standardizzazione del valori dei campi

L'utilizzo di valori "standard" permette la correlazione e il confronto tra fonti differenti di dati, e ne abilita l'interoperabilità. Per questo, i valori di certi campi di un dataset devono essere consistenti.

Da tenere in considerazione:

- È possibile sapere se una grandezza è grande o piccola solo se può essere confrontata con un'altra, tenendo conto di somiglianze e differenze, per esempio, tra serie di dati provenienti da fonti diverse.
- Lo [norma AENOR 137801:2015, Città intelligenti, Dati aperti](http://vocab.linkeddata.es/datosabiertos/) (ℹ è una norma spagnola. Questa guida è in parte una traduzione di un [testo spagnolo](https://datos.gob.es/en/documentacion/guia-practica-para-la-publicacion-de-datos-tabulares-en-archivos-csv)) considera tecnicamente corretti quei dati che, tra le altre caratteristiche:
    - Usano la stessa codifica e normalizzazione per lo stesso tipo di dati, pubblicati in diversi dataset di un catalogo. Per esempio, gli indirizzi sono sempre pubblicati con la stessa struttura, tipo, formato, in qualsiasi dataset e i dati geografici hanno lo stesso sistema di coordinate.
    - La codifica e la standardizzazione utilizzate si basano su alcuni standard comuni, riconosciuti e utilizzati da altre organizzazioni di codifica. Per esempio: norme approvate da [EUROSTAT](https://ec.europa.eu/eurostat/ramon/nomenclatures/index.cfm?TargetUrl=LST_NOM_DTL&StrNom=NACE_REV2&StrLanguageCode=ES&IntPcKey=&StrLayoutCode=HIERARCHIC&IntCurrentPage=1) o [INE](https://www.ine.es/ss/Satellite?L=0&c=Page&cid=1254735839296&p=1254735839296&pagename=MetodologiaYEstandares%2FINELayout).

- Si raccomanda:
    - Utilizzare vocabolari comunemente usati, per standardizzare la struttura e i valori delle informazioni pubblicate nei dataset[^1].
    - Nel caso in cui non si utilizzino vocabolari di riferimento, il valore assegnato a un dato attributo deve essere unico e coerente in tutta la tabella. In altre parole, se si sceglie di usare il valore "Barcellona" per riferirsi a questa città, non si dovrebbe usare ad esempio il valore "Città di Barcellona".

[^1]: Lo standard AENOR 137801:2015 include un elenco di vocabolari di riferimento: http://vocab.linkeddata.es/datosabiertos/


**Esempio**: standardizzazione del nome e del codice dell'attività economica.

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



In questo esempio, i valori del campo `codice_venditore` sono quelli corrispondenti alla [classificazione statistica EUROSTAT delle attività economiche della Comunità Europea](https://ec.europa.eu/eurostat/ramon/nomenclatures/index.cfm?TargetUrl=LST_NOM_DTL&StrNom=NACE_REV2&StrLanguageCode=ES&IntPcKey=&StrLayoutCode=HIERARCHIC&IntCurrentPage=1) (NACE Rev. 2), per la standardizzazione delle attività economiche dei concessionari di veicoli.
