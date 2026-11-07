---
hide:
# - toc
# - navigation
title: Cos'è un CSV
---

# Cos'è un CSV

CSV sta per *Comma Separated Values*, valori separati da virgole. È un file di testo che contiene una tabella: ogni riga del file è una riga della tabella, e i valori sono separati da un carattere, in questa guida la virgola.

Queste sono alcune colonne del [dataset delle biblioteche](../risorse/esempi/biblioteche.csv), l'esempio usato in tutta la guida. Nome della biblioteca, prestiti e spese sono inventati; codici Istat e nomi dei comuni sono veri.

``` title="Il file, aperto con un editor di testo"
codice_istat_comune,comune,biblioteca,prestiti,spesa_acquisti_euro
082053,Palermo,Biblioteca di esempio A,12450,8200.50
001168,None,Biblioteca di esempio B,3120,1250.00
019028,Cella Dati,Biblioteca di esempio C,,300.00
058091,Roma,Biblioteca di esempio D,20310,15400.75
```

E questa è la stessa cosa vista come tabella:

| codice_istat_comune | comune | biblioteca | prestiti | spesa_acquisti_euro |
| --- | --- | --- | --- | --- |
| 082053 | Palermo | Biblioteca di esempio A | 12450 | 8200.50 |
| 001168 | None | Biblioteca di esempio B | 3120 | 1250.00 |
| 019028 | Cella Dati | Biblioteca di esempio C | | 300.00 |
| 058091 | Roma | Biblioteca di esempio D | 20310 | 15400.75 |

## Righe, colonne, celle

- **Riga.** Descrive una cosa sola, qui una biblioteca.
- **Colonna.** Contiene una sola informazione, ripetuta per ogni riga, qui il nome del comune o i prestiti.
- **Cella.** È l'incrocio di una riga e di una colonna. Può essere vuota: la Biblioteca C non ha il dato dei prestiti, e fra le due virgole non c'è nulla.
- **Tabella.** È l'insieme delle righe. Un file ne contiene una sola.

Questa disposizione corrisponde alle regole note come *tidy data*, descritte da [Hadley Wickham nel 2014](https://www.jstatsoft.org/article/view/v059i10) e riprese dalle [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/allegato-B.html#csv): ogni riga è un'osservazione, ogni colonna è una variabile. Dati disposti così sono più facili da ordinare, filtrare e rappresentare.

## Cosa dice il formato

Il riferimento è la [RFC 4180](https://www.rfc-editor.org/rfc/rfc4180), un documento dell'*Internet Engineering Task Force* (IETF) che descrive il formato seguito dalla maggior parte dei programmi. Non è uno standard ufficiale: è un documento informativo. Dice che:

- ogni riga del file è un record, e termina con un'interruzione di riga, facoltativa solo per l'ultima;
- la prima riga può contenere i nomi delle colonne;
- tutte le righe dovrebbero avere lo stesso numero di valori, e dopo l'ultimo valore non c'è il separatore;
- gli spazi fanno parte del valore;
- i valori che contengono il separatore, virgolette o interruzioni di riga vanno racchiusi tra virgolette doppie;
- una virgoletta dentro un valore si scrive raddoppiata: `"la ""nuova"" sede"`.

Se il separatore è il carattere di tabulazione, il formato si chiama [TSV](https://www.iana.org/assignments/media-types/text/tab-separated-values).

## Cosa aggiunge questa guida

La RFC lascia aperte alcune scelte. Questa guida le chiude, e le regole ne spiegano il perché:

- la riga di intestazione deve esserci, e deve essere [una sola](linee_guida_pubblicazione/P01_unica_riga_intestazione.md);
- il separatore è la virgola e il separatore decimale è il [punto](linee_guida_pubblicazione/P11_campi_tipo_numerico.md);
- la codifica dei caratteri è UTF-8, meglio senza BOM (*Byte Order Mark*, tre byte invisibili all'inizio del file; un file che li contiene non è sbagliato);
- ogni colonna ha [un solo tipo di dato](linee_guida_pubblicazione/P07_tipi_dati.md);
- tutto ciò che non è un valore, come descrizioni, commenti e unità di misura, sta nel [dizionario dei dati](dizionario_dati.md), che dichiara anche separatore, delimitatore e codifica;
- per i nomi dei file è meglio usare lettere minuscole a-z, cifre 0-9 e il trattino basso `_` al posto degli spazi: si evitano problemi su server e programmi diversi.

Sul separatore la guida si scosta da altri testi: le [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/allegato-B.html#csv) riportano il suggerimento del documento europeo di usare il punto e virgola, perché la virgola compare spesso nei decimali. Con il punto come separatore decimale il problema non si pone.

!!! warning "Attenzione al doppio clic"

    Un file con la virgola, aperto con un doppio clic su un Excel che usa `;` come separatore di elenco, un'impostazione di Windows, finisce tutto in una sola colonna. Il file non è sbagliato: va aperto come spiega la pagina su [Excel e LibreOffice](linee_guida_pubblicazione/Linee_guida_importazione_esportazione.md#aprire-un-csv-in-excel-senza-rovinarlo).

## Glossario

- **Riga.** Una singola cosa descritta dalla tabella, per esempio una biblioteca. In altri testi si chiama record o osservazione.
- **Colonna.** Un'informazione che si ripete per ogni riga, per esempio il nome del comune. In altri testi si chiama campo o variabile.
- **Cella.** L'incrocio di una riga e di una colonna: contiene un valore oppure è vuota.
- **Intestazione.** La prima riga del file, con i nomi delle colonne.
- **Separatore.** Il carattere che divide i valori di una riga, in questa guida la virgola.
- **Delimitatore di testo.** Il carattere che racchiude un valore, di norma le virgolette doppie.
- **Codifica.** Il modo in cui i caratteri sono scritti nel file, per esempio UTF-8. Se è sbagliata, gli accenti si leggono male.
- **Dataset.** Uno o più file di dati pubblicati insieme, con la loro descrizione. In altri testi si chiama set di dati.
- **Dizionario dei dati.** Il documento che spiega ogni colonna: cosa contiene, di che tipo è, in quale unità di misura.
- **Schema.** Il dizionario dei dati scritto in un file che i programmi sanno leggere.
- **Metadati.** Le informazioni che descrivono un dataset nel catalogo: per esempio titolo, descrizione e licenza.
- **Risorsa.** Ciascun file di un dataset, nel linguaggio dei portali di dati.
- **Dati aperti.** Dati che chiunque può usare e riusare, in inglese *open data*. La definizione italiana è nel [CAD, art. 1, comma 1, lettera l-ter](https://www.normattiva.it/uri-res/N2Ls?urn:nir:stato:decreto.legislativo:2005-03-07;82~art1!vig=).
