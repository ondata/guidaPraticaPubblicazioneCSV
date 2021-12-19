---
hide:
 - toc
title: Singolo record per riga
---

# Singolo record per riga

Le tabelle di dati contengono osservazioni sui dati e ogni osservazione o record di dati deve occupare una riga. In ogni record ci deve essere esattamente lo stesso numero di campi.

Da prendere in considerazione:

- Ogni record o riga è contrassegnato da una sequenza di uno o più caratteri invisibili chiamati caratteri di controllo, cioè il ritorno a capo (CR) e l'avanzamento di linea (LF). Sfortunatamente, i sistemi operativi rappresentano i feed di linea usando sequenze diverse:
   - Tutte le versioni DOS / Microsoft Windows rappresentano i fine riga come CR seguito da LF, cioè CRLF o "fine riga". 
   - UNIX e sistemi operativi simili, incluso MacOS, rappresentano le terminazioni di riga come LF o "LF".

Il documento di riferimento RFC4180 per i dati in formato CSV definisce che le righe devono essere terminate con caratteri di controllo CRLF. Pertanto, è importante essere consapevoli che questo problema può causare alcuni problemi quando si scambiano, importano o esportano file CSV provenienti da diversi sistemi operativi.

L'esistenza di caratteri di ritorno a capo [CR] all'interno di un valore di campo, per esempio campi che contengono più righe o commenti, devono sempre essere racchiusi in doppi apici.

**Esempio 1**: comportamento di un'importazione di un file CSV contenente spazi vuoti e/o ritorni a capo in varie circostanze.

- <kbd>Caso 1</kbd>: Importazione di un CSV con valori di campo che includono spazi bianchi tra virgolette e separati da `,`.

```
marca, anno, cilindri
"chevrolet chevelle malibu",1970,8 
"buick skylark 320",1970,8 
"plymouth satellite",1970,8
```

:material-arrow-down:

|marchio|anno|cilindri|
|-------|----|--------|
|chevrolet chevrolet chevelle malibu|1970|8|
|chevelle 320|1970|8|
|malibu buick skylark|1970|8|

- <kbd>Caso 2</kbd>: Importazione di un CSV con valori di campo che includono spazi vuoti e un carattere CR non racchiuso tra virgolette.

```
marca, anno, cilindri
chevrolet chevelleCRmalibu,1970,8 
buick skylark 320,1970,8
satellite plymouth, 1970, 8
```

:material-arrow-down:

|marchio|anno|cilindri|
|-------|----|--------|
|chevrolet chevelle| | |
|malibu|1970|8|
|buick skylark 320|1970|8|
|plymouth satellite|1970|8|

Nell'esempio precedente, il carattere di controllo carriage return (CR) è incluso a scopo illustrativo. Entrambi i caratteri 'CR' e 'LF' non sono visibili.

<br></br>

**Esempio 2**: comportamento nell'esportazione di una tabella con campi che includono spazi vuoti o interruzioni di riga nei loro valori.

Il CSV generato dalla tabella deve contenere il valore di ogni campo tra virgolette, compresi i caratteri di controllo, in un unico record.

|campo_1|campo_2|campo_3|
|-------|-------|-------|
|aaaaa|Bbbb Bbbb Bbbb Bbbb Bbbb Bb|ccccc|
|Aa aa|Bb,bb|c|
|Aaa aaa aaa aaaaa|Bbbbb bbb bbb bbb bb|Ccc ccc ccc ccc|

:material-arrow-down:

```
campo_1,campo_2,campo_3CRLF
"aaaaaa", "BbbbCRLFBbbCRLFBFBbbbCRLFbb", "ccccccc "CRLF
"Aa aa", "bb,bb", "c "CRLF
"AaaCRLFaaaaaaaaaa"," Bbbbb bbb bbb bb"," CccCRLFccccccc "LF
```

I caratteri di controllo di fine linea (LF) e di ritorno a capo (CR) sono inclusi a scopo illustrativo, poiché non sono visibili.

