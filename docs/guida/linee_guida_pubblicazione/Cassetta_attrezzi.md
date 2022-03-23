---
hide:
 - toc
# - navigation
title: Cassetta degli attrezzi per i file CSV
---

Il tipo **`MIME`**[^1] più appropriato **per indicare il tipo di contenuto dei file `CSV`** trasmessi su Internet è indicato dal seguente valore della proprietà **`Content-Type:text/csv`**. Meno comunemente, è espresso usando la formula `Content-Type:application/octet-stream` oppure `Content-Type:text/comma-separated-values`.

Come indicato nel precedente capitolo, si raccomanda di **codificare i file `CSV` usando `UTF-8`**, se viene usato un altro tipo di codifica, questo può essere specificato attraverso il parametro `charset` nell'intestazione `Content-Type` ad esempio `Content-Type:text/csv;charset=ISO-8859-1`.

Se un file `CSV` **non contiene una riga di intestazione**, è possibile indicarlo usando il **parametro header del tipo `MIME`** ad esempio `Content-Type:text/csv;header=absent`.

L'**implementazione di queste proprietà** aiuta ad **elaborare i file `CSV` automaticamente** e coerentemente.

[^1]: [MIME Multipurpose Internet Mail Extensions](https://it.wikipedia.org/wiki/Multipurpose_Internet_Mail_Extensions)