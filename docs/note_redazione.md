---
hide:
# - toc
 - navigation
title: Note per chi scrive
---

# Note per chi scrive

## Come è fatta la guida

La guida è basata su [MkDocs](https://www.mkdocs.org/) e sul tema [Material](https://squidfunk.github.io/mkdocs-material/). Il testo è nella cartella `docs`. Prima di proporre una modifica, `mkdocs build --strict` deve terminare senza avvisi.

La cartella [risorse](https://github.com/ondata/guidaPraticaPubblicazioneCSV/tree/main/risorse) del repository contiene i file originali della guida spagnola.

## Per chi scriviamo

Chi in un ente ha i dati in un foglio di calcolo o in un gestionale, deve pubblicarli e non programma. I dettagli per chi usa il terminale o gli schemi stanno in un paragrafo a parte, in fondo, e non sono mai una condizione per capire la regola.

## Le schede delle regole

Ogni scheda ha, in quest'ordine:

1. il titolo con la regola all'imperativo;
2. una o due frasi con la regola, chiare anche senza il resto;
3. «Così sì e così no», con i riquadri `failure` e `success`;
4. «Perché», con una conseguenza concreta per chi riusa i dati;
5. «Casi particolari», solo se ce ne sono;
6. «Come si fa nel foglio di calcolo», solo se c'è qualcosa di utile e provato;
7. «Vedi anche», all'ultima riga.

Per la forza delle regole si usa «deve» per ciò che è obbligatorio per la guida, «meglio» o «è consigliato» per il consiglio.

## Gli esempi

C'è un solo esempio, il [dataset delle biblioteche](risorse/esempi/biblioteche.csv), con il suo [dizionario](risorse/esempi/biblioteche-dizionario.csv) e il suo [schema](risorse/esempi/biblioteche.schema.yaml). Nome della biblioteca, telefoni, spese e prestiti sono inventati, e lo si dice dove serve; codici Istat e nomi dei comuni sono veri.

- Le tabelle «Così sì» rispettano tutte le regole della guida, non solo quella della scheda.
- Gli esempi «Così no» mostrano un solo problema per volta, quando si può.
- Ogni tabella ha lo stesso numero di celle in tutte le righe. Ogni blocco CSV è un CSV valido e coerente con la tabella vicina.

## Stile

- Italiano semplice, frasi brevi, forma attiva, con un'immagine quando il concetto è astratto.
- Niente enfasi, superlativi e avverbi di rinforzo. Grassetti solo per il nome di una voce in un elenco.
- Solo il trattino della tastiera, `-`. Un paragrafo per riga, senza a capo forzati.
- Acronimi sciolti alla prima occorrenza.
- I titoli delle pagine non iniziano con un numero, a parte le schede.

## Titoli

La voce di menu di una scheda è una forma corta del titolo, per tenere il menu leggibile. Il titolo completo sta nell'intestazione della scheda e nell'elenco delle regole.

## Termini

| Si scrive | Non si scrive |
| --- | --- |
| colonna | campo, attributo, variabile |
| riga (una volta: «detta anche record») | osservazione |
| dataset | set di dati, insieme di dati |
| tabellare | tabulare |
| dizionario dei dati | dizionario di dati, dizionario dati |
| dati aperti | open data, salvo alla prima occorrenza |
| chi pubblica | editore |

Nei nomi degli standard restano i termini originali. Si evitano anche «buona prassi», «cattiva prassi», «digitare» e «quotato».

## Fatti e link

- Ogni fatto, norma, numero o comando va verificato prima di scriverlo. Se non si può verificare, non si scrive. I numeri portano la data della verifica.
- I link alle Linee guida AgID puntano alla [versione HTML](https://ondata.github.io/linee-guida-opendata/), alla sezione o al requisito precisi.
- Si collegano i capitoli fra loro: dove si legge «va spiegato nel dizionario», il link porta al [dizionario dei dati](guida/dizionario_dati.md).
