---
hide:
- toc
# - navigation
title: Campi di tipo data
---

# Campi di tipo data

Codificare le **date** utilizzando uno **standard** è fondamentale per facilitare l'analisi dei dati delle serie temporali. Lo **standard di riferimento** è quello **definito dalla norma [ISO8601](https://es.wikipedia.org/wiki/ISO_8601)**, che codifica i valori di data con il formato `YYYYY-MM-DD`, nella sua forma abbreviata, o `YYYYY-MM-DDTHH:MM:SS`, nella sua versione estesa.

## Date

Nel caso delle date è utile utilizzare le seguenti raccomandazioni:

- riempire di zeri i valori 0-9 per indicare `MM`, `DD`, `HH`, `MM` e `SS`, poiché  ogni valore deve avere un numero fisso di cifre;
- usare `-` come separatore per le date e `:` per le ore;
- usare la lettera `T` come carattere separatore tra una data e un'ora quando usi la versione estesa;
- usare preferibilmente le date complete `AAAA-MM-GG` piuttosto che indicare solo i mesi o gli anni quando i dati lo consentono;
- se sono disponibili solo dati mensili, l'opzione migliore quella di includere una data completa riferita all'ultimo giorno del mese; per esempio, per settembre `2019-09-30`;
- se la data completa non può essere inclusa è preferibile esprimere l'anno e il mese in colonne separate (colonna `anno` e colonna `mese`).

## Ore

Nel caso delle ore è utile utilizzare le seguenti raccomandazioni:

- usare preferibile il formato 24 ore `HH:MM:SS` piuttosto che il formato 12 ore `HH:MM:SS AM/PM`;
- usare un unico campo per includere i valori che rappresentano la data e l'ora combinate usando il formato `YYYYY-MM-DDTHH:MM:SS`.

### Esempio 1:

campi con date in forma breve

!!! failure "Cattiva prassi"

    | marchio | data_lancio |
    | --- | --- |
    | chevrolet chevelle malibu | Gennaio 1970 |
    | buick skylark 320 | 23/07/1970 |
    | plymouth satellite | 1 febbraio 1970 |

!!! success "Buona prassi"

    | marchio | data_lancio |
    | --- | --- |
    | chevrolet chevelle malibu | 1970-01-31 |
    | buick skylark 320 | 1970-07-23 |
    | plymouth satellite | 1970-02-01 |


### Esempio 2:

campi con date e orari in forma estesa

!!! failure "Cattiva prassi"

    | identificativo_veicolo | data_vendita |
    | --- | --- |
    | 0003407G236 | 12 gennaio 1970, alle 15:10 |
    | 0003507H003 | 23/07/1970 - 04:34 PM |
    | 0003407G237 | 1-Febbraio-1970-12-23-34 |

!!! success "Buona prassi"

| identificativo_veicolo | data_vendita |
    | --- | --- |
    | 0003407G236 | 1970-01-31T15:10:00 |
    | 0003507H003 | 1970-07-23T16:34:00 |
    | 0003407G237 | 1970-02-01T12:23:34 |
    