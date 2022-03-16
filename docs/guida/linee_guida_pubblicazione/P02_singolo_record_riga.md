---
hide:
 - toc
# - navigation
title: Singolo record per riga
---

# Singolo record per riga

Le tabelle di dati contengono osservazioni sui dati e ogni osservazione o *record* di dati deve occupare una riga. In ogni *record* ci deve essere esattamente lo stesso numero di campi.

Da prendere in considerazione:

- Ogni *record* o riga è contrassegnato da una sequenza di uno o più caratteri invisibili, chiamati caratteri di controllo, il ritorno a capo (`CR`, *carriage return*) e l'avanzamento di linea (`LF`, *line feed*). Sfortunatamente, i sistemi operativi li rappresentano usando sequenze diverse:
    - Tutte le versioni DOS / Microsoft Windows rappresentano i fine riga come `CR` seguito da `LF`, cioè `CRLF` ovvero `\r\n`.
    - UNIX e sistemi operativi simili, incluso MacOS, rappresentano le terminazioni di riga come LF ovvero `\n`.

Il documento di riferimento `RFC4180`[^1] per i dati in formato CSV riporta che le righe devono terminare con caratteri di controllo `CRLF`. Pertanto, è importante essere consapevoli che questo, può causare alcuni problemi quando si scambiano, importano o esportano file CSV provenienti da diversi sistemi operativi.

L'esistenza di caratteri di ritorno a capo `CR` all'interno di un valore di campo - per esempio campi che contengono più righe o commenti - impone che questo debba essere racchiuso tra virgolette (`"`).

[^1]: [Common Format and MIME Type for Comma-Separated Values (CSV) Files](https://datatracker.ietf.org/doc/html/rfc4180)

### Esempio 1: importare un file CSV contenente spazi vuoti e/o ritorni a capo in varie circostanze.

#### Caso 1: Importare un CSV con valori di campo che includono spazi bianchi tra virgolette e separati da `,`.


```
marca, anno, cilindri
"chevrolet chevelle malibu",1970,8
"buick skylark 320",1970,8
"plymouth satellite",1970,8
```

:material-arrow-down:

!!! success "Importazione corretta"

    |marca|anno|cilindri|
    |-------|----|--------|
    |chevrolet chevrolet chevelle malibu|1970|8|
    |chevelle 320|1970|8|
    |malibu buick skylark|1970|8|

#### Caso 2: Importare un CSV con valori di campo che includono spazi vuoti e un carattere CR non racchiuso tra virgolette.

```
marca, anno, cilindri
chevrolet chevelleCRmalibu,1970,8
buick skylark 320,1970,8
satellite plymouth, 1970, 8
```

:material-arrow-down:

!!! error "Importazione problematica"

    |marca|anno|cilindri|
    |-------|----|--------|
    |chevrolet chevelle| | |
    |malibu|1970|8|
    |buick skylark 320|1970|8|
    |plymouth satellite|1970|8|

Nell'esempio precedente, il carattere di controllo *carriage return* (`CR`) è incluso a scopo illustrativo. Entrambi i caratteri `CR` e `LF` non sono visibili.

**Esempio 2**: comportamento nell'esportazione di una tabella con campi che includono spazi vuoti o interruzioni di riga nei loro valori.

Il CSV generato dalla tabella deve contenere il valore di ogni campo tra virgolette, compresi i caratteri di controllo, in un unico record.

|campo_1|campo_2|campo_3|
|-------|-------:|-------:|
|aaaaa|Bbbb<br>Bbb<br>Bbbb<br>Bb|ccccc|
|Aa aa|Bb,bb|c|
|Aaa<br>aaaaa|Bbbbb bbb bbb bbb bb|Ccc<br>ccccc|

:material-arrow-down:

```
campo_1,campo_2,campo_3CRLF
"aaaaa", "BbbbCRLFBbbCRLFBbbbCRLFbb","ccccc"CRLF
“Aa aa”,” bb,bb”,”c”CRLF
“AaaCRLFaaaaaa”,” Bbbbb bbb bb”,” CccCRLFccccc”LF
```

I caratteri di controllo di fine linea (`LF`) e di ritorno a capo (`CR`) sono inclusi a scopo illustrativo, poiché non sono visibili.

