---
hide:
- toc
# - navigation
title: Campi di tipo testo
---

I campi di tipo testo devono contenere stringhe di testo senza spazi vuoti iniziali o finali; gli eventuali caratteri (spazi o tabulazioni) adiacenti ai separatori di campo saranno ignorati.

## In generale:
I campi di testo possono sempre essere delimitati da virgolette (`"`) e le applicazioni che eseguono operazioni di lettura dei dati analizzeranno e scarteranno tali delimitatori.

Da prendere in considerazione:

se il valore di un campo contiene una qualsiasi stringa di testo che appartiene ad uno dei seguenti casi, deve essere trattato come indicato:

- se gli spazi bianchi all'inizio o alla fine di una stringa di testo sono significativi e devono essere preservati, il campo deve essere delimitato da virgolette (`"`);
- se la stringa include una o più virgole il campo deve essere delimitato da doppi apici;
- se la stringa include del testo quotato le virgolette (`"`) devono essere duplicate e il campo deve essere delimitato da virgolette (`"`);
- se la stringa include delle interruzioni di riga il campo deve essere racchiuso tra virgolette (`"`).

### Esempio 1:
comportamento nell'esportazione di una tabella con valori contenenti spazi vuoti (iniziali o finali), quando si esporta la tabella come CSV, i valori vuoti scompaiono.

| marca | anno | cilindri |
| --- | --- | ---: |
| BBBBBBchevrolet chevelle malibu | 1970 | 8 |
| BBBBBBbuick skylark 320BBBB | 1970 | 8 |
| plymouth satellite | 1970 | 8 |

Nell'esempio precedente, gli spazi bianchi sono visualizzati attraverso il carattere (`B`) a scopo illustrativo, gli spazi bianchi non sono visualizzati attraverso un carattere.

```
marca,anno,cilindri
"chevrolet chevelle malibu",1970,8
"buick skylark 320",1970,8
"plymouth satellite",1970,8
```

### Esempio 2:
comportamento dell'importazione di un file CSV con valori contenenti spazi vuoti (iniziali o finali) e caratteri quotati.

```
campo1,campo2,campo3
"valore del campo1","   valore del campo2 con spazi iniziali","valore del campo ""3"" che include un dato dentro doppie virgolette"
```

| campo1 | campo2 | campo3 |
| --- | --- | --- |
| valore del campo1 | ␣␣␣valore del campo2 | valore del campo "3" che include un dato dentro doppie virgolette |

Qui sopra, gli spazi bianchi sono visualizzati attraverso il carattere (`␣`) a scopo illustrativo, gli spazi bianchi non sono visualizzati attraverso un carattere.
