---
hide:
 - toc
# - navigation
title: Come servire i file via web
---

# Come servire i file via web

Quando un programma scarica il tuo CSV, il server gli dice di che tipo di file si tratta, con l'intestazione HTTP `Content-Type`. È l'etichetta sulla scatola: se è giusta, il programma sa come aprirla senza tirare a indovinare.

Se pubblichi su un portale, questa impostazione non dipende da te: la pagina ti serve per sapere che cosa chiedere a chi lo gestisce.

## L'intestazione da usare

```
Content-Type: text/csv; charset=utf-8; header=present
```

- **`text/csv`.** È il tipo [registrato](https://www.iana.org/assignments/media-types/text/csv) per i CSV. Non usare `application/octet-stream`, che indica un generico file binario, né `text/comma-separated-values`, che nel [registro IANA](https://www.iana.org/assignments/media-types/media-types.xhtml#text) non c'è.
- **`charset`.** Indica la codifica. La [RFC 7111](https://www.rfc-editor.org/rfc/rfc7111) chiede di indicarla e, se manca, di assumere UTF-8. Per un file ereditato in un'altra codifica si scrive quella, per esempio `charset=ISO-8859-1`.
- **`header`.** Dice se c'è la riga di intestazione: `present` o `absent`. Il valore `header=absent` serve solo per un file ereditato senza intestazione, cosa [da evitare](P01_unica_riga_intestazione.md).

## Come controllare

```
curl -sI https://ondata.github.io/guidaPraticaPubblicazioneCSV/risorse/esempi/biblioteche.csv | grep -i content-type
```

Il comando mostra quello che il server dichiara davvero. Se la risposta è diversa da `text/csv`, chiedi di correggerla a chi gestisce il server o il portale.

Su GitHub conta l'indirizzo da cui si serve il file. Con lo stesso file, il 7 novembre 2026, GitHub Pages rispondeva `text/csv; charset=utf-8`, mentre `raw.githubusercontent.com` rispondeva `text/plain; charset=utf-8`. Per pubblicare un CSV da GitHub è meglio quindi usare l'indirizzo di GitHub Pages.

## Collegare il dizionario e lo schema

Metti il link al [dizionario dei dati](../dizionario_dati.md) e all'eventuale schema nella pagina del dataset, accanto al file.

Con CSVW il server può anche indicare lo schema nella risposta, come descrive la [specifica del W3C](https://www.w3.org/TR/tabular-data-model/#link-header):

```
Link: <biblioteche.csv-metadata.json>; rel="describedby"; type="application/csvm+json"
```

Se questa intestazione manca, la stessa specifica prevede che i programmi cerchino il file `biblioteche.csv-metadata.json` accanto al CSV.

## Versioni a un indirizzo stabile

Quando un dataset cambia, chi lo ha usato deve poter ritrovare la versione che aveva. Le [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/capitolo-5.html#sec-modellazione-e-documentazione) raccomandano che le versioni siano accessibili a un URL stabile, documentato con la pubblicazione del dato. Un modo semplice è tenere l'indirizzo dell'ultima versione sempre uguale e mettere accanto i file datati, per esempio `biblioteche-2023.csv`.

## File molto grandi

Il CSV resta il formato di riferimento. Per file molto grandi si può aggiungere una versione compressa (`.csv.gz`) e una in Parquet, che conserva i tipi delle colonne: sono complementi del CSV e non lo sostituiscono.
