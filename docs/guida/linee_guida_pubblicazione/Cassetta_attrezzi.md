---
hide:
# - toc
# - navigation
title: Strumenti di controllo
---

# Strumenti di controllo

Prima di pubblicare un CSV conviene controllarlo. Gli strumenti possono anche sbagliare senza dirlo: i casi sono in fondo alla pagina.

## Senza terminale

- **Editor di testo.** È il primo controllo, e c'è già su ogni computer (su Windows, Blocco note). Mostra il file com'è, senza che un programma lo interpreti: guarda se ci sono ancora gli zeri iniziali dei codici e il `+` dei telefoni, qual è il separatore, se sopra l'intestazione ci sono righe di titolo. Si apre e si chiude senza salvare.
- **[CSV Lint](https://csvlint.io/).** È un servizio online ospitato dall'Open Data Institute, che non chiede installazioni. Controlla che il file sia leggibile e ben formato, e distingue errori, avvertimenti e consigli. Ha due avvertenze. Il file finisce su un servizio esterno, che dichiara di cancellarlo dopo il controllo: non caricare file con [dati personali](Dati_personali.md) non ancora pubblicabili. E segnala come errore «Whitespace» il BOM che Excel aggiunge salvando in «CSV UTF-8»: non è un problema dei dati.
- **[LibreOffice Calc](https://www.libreoffice.org/download/download-libreoffice/).** Va installato ed è gratuito. Quando apre un CSV mostra una finestra in cui scegliere codifica, separatore e tipo di ogni colonna: impostando come testo le colonne di codici, telefoni e mesi, zeri e `+` restano. Quando salvi, controlla il set di caratteri: può proporre un'altra codifica, e va scelto UTF-8. La procedura è nella pagina su [Excel e LibreOffice](Linee_guida_importazione_esportazione.md).
- **[OpenRefine](https://openrefine.org/download).** Va installato ed è gratuito. Serve a pulire i dati e a raggruppare i valori simili, per [scrivere la stessa cosa sempre allo stesso modo](P08_standardizzazione_valori_campi.md). I dati restano sul tuo computer. Non lo abbiamo provato sui file di questa guida.

## Per chi usa il terminale

I comandi sono stati provati l'8 novembre 2026 su Linux e su varianti del [file delle biblioteche](../../risorse/esempi/biblioteche.csv), con DuckDB 2.0.0, Miller 6.22.0 e Frictionless 5.21.0. I comandi di DuckDB e di Miller sono stati provati anche su Windows, con PowerShell 7. `file` e `iconv` ci sono su Linux, macOS e WSL.

`export.csv` è l'esportazione di un gestionale italiano: separatore `;`, virgola decimale, codifica Windows-1252. Al posto di questi nomi di esempio metti i nomi dei tuoi file e delle tue colonne.

### Installare gli strumenti

Bastano tre strumenti. [DuckDB](https://duckdb.org/install/) e [Miller](https://miller.readthedocs.io/en/latest/installing-miller/) si installano seguendo le loro pagine, Frictionless con [uv](https://docs.astral.sh/uv/getting-started/installation/):

```
uv tool install frictionless
```

### Codifica

Vedere la codifica. `charset=utf-8` e `charset=us-ascii` vanno bene: un file UTF-8 senza accenti risulta `us-ascii`. Qualunque altro valore, come `iso-8859-1` o `unknown-8bit`, indica un file che non è in UTF-8.

```
file -bi export.csv
```

Controllare che il file sia davvero in UTF-8. Se non lo è, il comando risponde `illegal input sequence` con la posizione.

```
iconv -f UTF-8 -t UTF-8 export.csv > /dev/null
```

Convertire in UTF-8 un file salvato da Excel come «CSV».

```
iconv -f WINDOWS-1252 -t UTF-8 export.csv > export_utf8.csv
```

Lo stesso su Windows, con PowerShell 7.

```
Get-Content export.csv -Encoding windows-1252 | Set-Content export_utf8.csv -Encoding utf8NoBOM
```

Togliere il BOM. I valori non cambiano.

```
mlr --csv cat con_bom.csv > senza_bom.csv
```

### Struttura

Trovare le righe con un numero di valori diverso dall'intestazione, con il numero di riga del file e il tipo di errore. Le righe buone restano.

```
duckdb -csv -c "from read_csv('rotto.csv',delim=',',header=true,store_rejects=true,all_varchar=true); select line,error_type,csv_line from reject_errors;"
```

Riconoscere separatore e colonne. Da solo non basta: vedi le trappole.

```
duckdb -c "from sniff_csv('export_utf8.csv')"
```

### Contenuto delle colonne

Vedere per ogni colonna minimo, massimo, valori distinti e percentuale di celle vuote.

```
duckdb -c "summarize select * from read_csv('biblioteche.csv',delim=',',header=true,all_varchar=true)"
```

Lo stesso con Miller, con il tipo e la lunghezza dei valori.

```
mlr --icsv --opprint summary -a field_type,null_count,distinct_count,minlen,maxlen biblioteche.csv
```

Trovare gli zeri iniziali persi. In un codice a lunghezza fissa, più di una lunghezza è il segnale.

```
duckdb -csv -c "select length(codice_istat_comune) lunghezza,count(*) righe from read_csv('biblioteche.csv',delim=',',header=true,all_varchar=true) group by 1"
```

Trovare i valori che non stanno in un elenco ammesso. `dug_ammessi.csv` ha una colonna `dug`.

```
duckdb -csv -c "select t.biblioteca,t.dug from read_csv('biblioteche.csv',delim=',',header=true,all_varchar=true) t anti join read_csv('dug_ammessi.csv',delim=',',header=true,all_varchar=true) v on t.dug=v.dug"
```

Validare il file con uno [schema](../dizionario_dati.md). Gli errori hanno il numero di riga e il nome della colonna. Per un file con `;` si aggiunge `--dialect '{"delimiter":";"}'`.

```
frictionless validate biblioteche.csv --schema biblioteche.schema.yaml --encoding utf-8
```

### Un controllo per regola

Ogni comando cerca le violazioni di una regola e non cambia il file. Se mostra solo l'intestazione, il controllo è passato. Sono scritti per il file delle biblioteche: cambia i nomi delle colonne con i tuoi.

Nomi di colonna ([regola 3](P03_denominazione_colonne.md)): minuscole, cifre e trattini bassi, con una lettera all'inizio.

```
duckdb -csv -c "select column_name from (describe from read_csv('biblioteche.csv',delim=',',header=true,all_varchar=true)) where not regexp_matches(column_name,'^[a-z][a-z0-9_]*$')"
```

Totali mescolati ai dati ([regola 6](P06_subtotali_totali_raggruppamenti.md)). È un indizio, non una prova: cerca la parola «totale» e le righe senza comune.

```
duckdb -csv -c "from read_csv('biblioteche.csv',delim=',',header=true,all_varchar=true) where biblioteca ilike '%totale%' or comune is null"
```

Spazi prima o dopo un valore ([regola 10](P10_campi_tipo_testo.md)), con la riga del file e la colonna.

```
mlr --icsv --ocsv put -q 'for (k,v in $*) { if (string(v) != strip(string(v))) { emit1 {"riga":NR+1,"colonna":k,"valore":v} } }' biblioteche.csv
```

Numeri che non hanno il punto decimale ([regola 11](P11_campi_tipo_numerico.md)).

```
duckdb -csv -c "select biblioteca,spesa_acquisti_euro from read_csv('biblioteche.csv',delim=',',header=true,all_varchar=true) where spesa_acquisti_euro is not null and try_cast(spesa_acquisti_euro as double) is null"
```

Date non scritte come `AAAA-MM-GG` ([regola 12](P12_campi_tipo_data.md)), comprese quelle impossibili come `2010-02-31`. Una data incompleta come `2023-07` viene segnalata anche se può essere corretta.

```
duckdb -csv -c "select biblioteca,data_apertura from read_csv('biblioteche.csv',delim=',',header=true,all_varchar=true) where data_apertura is not null and try_strptime(data_apertura,'%Y-%m-%d') is null"
```

Telefoni non in formato internazionale ([regola 13](P13_campi_tipo_numero_telefonico.md)).

```
duckdb -csv -c "select biblioteca,telefono from read_csv('biblioteche.csv',delim=',',header=true,all_varchar=true) where not regexp_matches(telefono,'^\+[0-9]+$')"
```

CAP che non hanno 5 cifre ([regola 14](P14_campi_tipo_indirizzo_postale.md)).

```
duckdb -csv -c "select biblioteca,cap from read_csv('biblioteche.csv',delim=',',header=true,all_varchar=true) where not regexp_matches(cap,'^[0-9]{5}$')"
```

Coordinate fuori dall'Italia, invertite o con la virgola ([regola 15](P15_campi_con_coordinate_geografiche.md)). I limiti sono un rettangolo che contiene l'Italia.

```
duckdb -csv -c "select biblioteca,latitudine,longitudine from read_csv('biblioteche.csv',delim=',',header=true,all_varchar=true) where try_cast(latitudine as double) not between 35 and 48 or try_cast(longitudine as double) not between 6 and 19 or try_cast(latitudine as double) is null or try_cast(longitudine as double) is null"
```

Lettere accentate scritte in forma scomposta. Una `à` può essere un solo carattere oppure una `a` seguita dall'accento: a vista sono uguali, ma per un programma sono valori diversi. Meglio pubblicare la forma composta (NFC).

```
duckdb -csv -c "select comune from read_csv('biblioteche.csv',delim=',',header=true,all_varchar=true) where comune <> nfc_normalize(comune)"
```

### Portare il file al formato della guida

Passare da `;` e virgola decimale a `,` e punto decimale, togliendo il separatore delle migliaia. I codici restano testo.

```
mlr -S --csv --ifs ';' --ofs ',' put '$spesa_acquisti_euro=sub(gsub($spesa_acquisti_euro,"\.",""),",","."); $prestiti=gsub($prestiti,"\.","")' export_utf8.csv
```

Lo stesso con DuckDB, che scrive un nuovo file.

```
duckdb -c "copy (select * replace (replace(replace(spesa_acquisti_euro,'.',''),',','.') as spesa_acquisti_euro, replace(prestiti,'.','') as prestiti) from read_csv('export_utf8.csv',delim=';',header=true,all_varchar=true)) to 'pulito.csv' (header, delimiter ',')"
```

Riscrivere le date come `AAAA-MM-GG`. Una cella vuota resta vuota. Una data impossibile come `31/02/2010` diventa `(error)`, quindi si vede.

```
mlr --icsv --ifs ';' --ocsv --ofs ';' put 'is_not_empty($data_apertura){$data_apertura=strftime(strptime($data_apertura,"%d/%m/%Y"),"%Y-%m-%d")}' export_utf8.csv
```

Le date impossibili si possono cercare anche prima di convertire.

```
duckdb -csv -c "select biblioteca,data_apertura from read_csv('export_utf8.csv',delim=';',header=true,all_varchar=true) where data_apertura is not null and try_strptime(data_apertura,'%d/%m/%Y') is null"
```

Passare [dalle colonne alle righe](P04_strutture_dati_verticale_orizzontale.md), con un file che ha una colonna per anno.

```
mlr --csv reshape -r '^[0-9]{4}$' -o anno,prestiti largo.csv
```

Lo stesso con DuckDB.

```
duckdb -csv -c "unpivot (from read_csv('largo.csv',delim=',',header=true,all_varchar=true)) on columns(* exclude comune) into name anno value prestiti"
```

### Confrontare due versioni

Vedere le righe nuove o cambiate.

```
duckdb -csv -c "from read_csv('v2.csv',delim=',',header=true,all_varchar=true) except from read_csv('v1.csv',delim=',',header=true,all_varchar=true)"
```

Vedere le righe tolte o cambiate.

```
duckdb -csv -c "from read_csv('v1.csv',delim=',',header=true,all_varchar=true) except from read_csv('v2.csv',delim=',',header=true,all_varchar=true)"
```

Vedere prima e dopo di una colonna, per le righe presenti in entrambe le versioni. La colonna in `using` deve identificare la riga.

```
duckdb -csv -c "select biblioteca,v1.prestiti prima,v2.prestiti dopo from read_csv('v1.csv',delim=',',header=true,all_varchar=true) v1 join read_csv('v2.csv',delim=',',header=true,all_varchar=true) v2 using (biblioteca) where v1.prestiti is distinct from v2.prestiti"
```

### Leggere un CSV senza alterarlo

Chi riusa i dati può perdere zeri iniziali e valori come `NA` e `None`, se il programma deduce i tipi. Con DuckDB si usa `all_varchar=true`, come in tutti i comandi di questa pagina. Con pandas, una libreria di Python:

```python
import pandas as pd
dati = pd.read_csv("biblioteche.csv", dtype=str, keep_default_na=False)
```

## Trappole

Gli strumenti possono sbagliare in silenzio. Questi sono i casi che abbiamo misurato sui file di prova.

- **Frictionless, schema con percorso assoluto.** Rifiuta lo schema (`path ... is not safe`) e il file risulta `INVALID` anche se i dati sono corretti. Lancia il comando dalla cartella del file, con un percorso relativo.
- **DuckDB, senza `delim` e `header`.** Su un file con righe di lunghezza diversa mette tutto in una sola colonna, senza errori. Su un file con le colonne `comune,2021,2022,2023` non riconosce l'intestazione e nomina le colonne `column0`, `column1` e così via. Scrivi sempre `delim=',',header=true`.
- **Frictionless, senza `--encoding utf-8`.** Dà `VALID` a un file in Windows-1252.
- **Frictionless, senza schema.** Controlla solo la struttura: dà `VALID` a un codice Istat senza lo zero iniziale, o a un CAP di tre cifre. Quando deduce lo schema da solo, considera `codice_istat_comune` un numero intero.
- **`iconv -f ISO-8859-1`.** Su un file di Excel rovina il simbolo `€` senza segnalare errori. Usa `WINDOWS-1252`.
- **`awk` per contare le colonne.** Su una riga con `"chiusa, per lavori"` conta 3 valori invece di 2, perché non conosce le virgolette.
- **Testi inseriti da terzi.** Se una colonna raccoglie segnalazioni o commenti, controlla i valori che iniziano con `=`, `+`, `-` o `@`: un foglio di calcolo può [interpretarli come formule](https://owasp.org/www-community/attacks/CSV_Injection). Nella nostra prova Excel ha trasformato `+39-0515270001` in un calcolo. Non vanno cambiati i dati per questo: un telefono scritto come `+390910000001` è corretto.

```
duckdb -csv -c "select biblioteca,note from read_csv('segnalazioni.csv',delim=',',header=true,all_varchar=true) where regexp_matches(note,'^[=+@-]')"
```
