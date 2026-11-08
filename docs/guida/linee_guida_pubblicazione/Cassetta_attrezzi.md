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
- **[LibreOffice Calc](https://www.libreoffice.org/download/download-libreoffice/).** Va installato ed è gratuito. Quando apre un CSV mostra una finestra in cui scegliere codifica, separatore e tipo di ogni colonna: impostando come testo le colonne di codici, telefoni e mesi, zeri e `+` restano. Quando salvi, controlla il set di caratteri: nella nostra prova proponeva ISO-8859-1, e va scelto UTF-8. La procedura è nella pagina su [Excel e LibreOffice](Linee_guida_importazione_esportazione.md).
- **[OpenRefine](https://openrefine.org/download).** Va installato ed è gratuito. Serve a pulire i dati e a raggruppare i valori simili, per [scrivere la stessa cosa sempre allo stesso modo](P08_standardizzazione_valori_campi.md). I dati restano sul tuo computer. Non lo abbiamo provato sui file di questa guida.

## Per chi usa il terminale

I comandi sono stati provati il 7 novembre 2026 su Linux, su varianti del [file delle biblioteche](../../risorse/esempi/biblioteche.csv), con DuckDB 2.0.0, Miller 6.22.0, Frictionless 5.21.0, csvkit 2.2.0 e daff 1.4.2. Non li abbiamo provati su Windows, salvo il comando di PowerShell.

`export.csv` è l'esportazione di un gestionale italiano: separatore `;`, virgola decimale, codifica Windows-1252. Al posto di questi nomi di esempio metti i nomi dei tuoi file e delle tue colonne.

### Installare gli strumenti

[DuckDB](https://duckdb.org/install/) e [Miller](https://miller.readthedocs.io/en/latest/installing-miller/) si installano seguendo le loro pagine. Gli altri si installano con [uv](https://docs.astral.sh/uv/getting-started/installation/):

```
uv tool install frictionless
uv tool install csvkit
uv tool install daff
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

Togliere il BOM.

```
sed '1s/^\xEF\xBB\xBF//' con_bom.csv > senza_bom.csv
```

### Struttura

Trovare le righe con un numero di valori diverso dall'intestazione.

```
csvclean --length-mismatch rotto.csv
```

Le stesse righe, con il numero di riga del file e il tipo di errore. Le righe buone restano.

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

Passare [dalle colonne alle righe](P04_strutture_dati_verticale_orizzontale.md), con un file che ha una colonna per anno.

```
mlr --csv reshape -r '^[0-9]{4}$' -o anno,prestiti largo.csv
```

### Confrontare due versioni

Vedere righe cambiate, nuove e tolte.

```
daff v1.csv v2.csv
```

Vedere solo le righe nuove o cambiate.

```
duckdb -csv -c "from read_csv('v2.csv',delim=',',header=true,all_varchar=true) except from read_csv('v1.csv',delim=',',header=true,all_varchar=true)"
```

## Trappole

Gli strumenti possono sbagliare in silenzio. Questi sono i casi che abbiamo misurato sui file di prova.

- **Frictionless, schema con percorso assoluto.** Rifiuta lo schema (`path ... is not safe`) e il file risulta `INVALID` anche se i dati sono corretti. Lancia il comando dalla cartella del file, con un percorso relativo.
- **DuckDB, senza `delim` e `header`.** Su un file con righe di lunghezza diversa mette tutto in una sola colonna, senza errori. Su un file con le colonne `comune,2021,2022,2023` non riconosce l'intestazione e nomina le colonne `column0`, `column1` e così via. Scrivi sempre `delim=',',header=true`.
- **Frictionless, senza `--encoding utf-8`.** Dà `VALID` a un file in Windows-1252.
- **Frictionless, senza schema.** Controlla solo la struttura: dà `VALID` a un codice Istat senza lo zero iniziale, o a un CAP di tre cifre. Quando deduce lo schema da solo, considera `codice_istat_comune` un numero intero.
- **`iconv -f ISO-8859-1`.** Su un file di Excel rovina il simbolo `€` senza segnalare errori. Usa `WINDOWS-1252`.
- **`awk` per contare le colonne.** Su una riga con `"chiusa, per lavori"` conta 3 valori invece di 2, perché non conosce le virgolette.
- **`csvlook` e `csvstat`.** Deducono i tipi: con `csvlook`, `082053` diventa `82,053`, `12.450` diventa `12.45` e `300,00` diventa `30,000.000`. L'opzione `-I` evita queste conversioni. Anche con `-I`, però, `csvlook` mostra vuota la cella del comune di `None`, un comune vero.
- **`csvclean`.** Il numero che riporta è quello della riga di dati, non della riga del file: dove `csvclean` dice `2`, la riga del file è la 3.
- **Testi inseriti da terzi.** Se una colonna raccoglie segnalazioni o commenti, controlla i valori che iniziano con `=`, `+`, `-` o `@`: un foglio di calcolo può [interpretarli come formule](https://owasp.org/www-community/attacks/CSV_Injection). Nella nostra prova Excel ha trasformato `+39-0515270001` in un calcolo. Non vanno cambiati i dati per questo: un telefono scritto come `+390910000001` è corretto.

```
duckdb -csv -c "select biblioteca,note from read_csv('segnalazioni.csv',delim=',',header=true,all_varchar=true) where regexp_matches(note,'^[=+@-]')"
```
