---
hide:
 - toc
# - navigation
title: Affianca una descrizione ai codici
---

# 9. Affianca una descrizione ai codici

Quando una colonna contiene un codice, è consigliato affiancarle una colonna con la descrizione: `codice_istat_comune` e `comune`. Un codice fatto di cifre è un testo, non un numero: non ci si fanno operazioni e gli zeri iniziali contano.

## Così sì e così no

Nomi delle biblioteche e prestiti sono inventati, i codici Istat e i nomi dei comuni sono veri. Qui c'è solo il codice: chi legge deve cercare altrove di quale comune si tratta.

!!! failure "Così no"

    | codice_istat_comune | biblioteca | prestiti |
    | --- | --- | ---: |
    | 082053 | Biblioteca di esempio A | 12450 |
    | 001168 | Biblioteca di esempio B | 3120 |
    | 058091 | Biblioteca di esempio D | 20310 |

!!! success "Così sì"

    | codice_istat_comune | comune | biblioteca | prestiti |
    | --- | --- | --- | ---: |
    | 082053 | Palermo | Biblioteca di esempio A | 12450 |
    | 001168 | None | Biblioteca di esempio B | 3120 |
    | 058091 | Roma | Biblioteca di esempio D | 20310 |

Qui il codice è stato trattato come un numero e ha perso gli zeri iniziali.

!!! failure "Così no"

    | codice_istat_comune | comune | biblioteca | prestiti |
    | ---: | --- | --- | ---: |
    | 82053 | Palermo | Biblioteca di esempio A | 12450 |
    | 1168 | None | Biblioteca di esempio B | 3120 |
    | 58091 | Roma | Biblioteca di esempio D | 20310 |

## Perché

I codici sono utili per filtrare, riassumere, ordinare e unire i dati, ma chi non li conosce non sa interpretarli se non sono spiegati. Con la descrizione accanto il file si legge senza aprire altri documenti, e il codice resta disponibile per i programmi.

Un codice senza zeri non è più lo stesso codice: `82053` non corrisponde a `082053`, e chi prova a unire il tuo file a un elenco ufficiale dei comuni perde quelle righe.

## Casi particolari

- **Codici di cifre.** La regola vale per codici Istat, CAP, codici fiscali e di attività. Dichiara queste colonne come testo nel [dizionario dei dati](../dizionario_dati.md) e controlla che gli zeri siano ancora lì prima di pubblicare, aprendo il file con un editor di testo.
- **Comune come territorio.** Per l'Italia il codice è quello Istat del comune, di 6 caratteri ([SITUAS](https://situas.istat.it/web/), il Sistema informativo territoriale delle unità amministrative e statistiche), e la colonna `comune` contiene il suo nome.
- **Comune come ente.** Se la colonna indica invece l'amministrazione che ha prodotto il dato o che eroga un servizio, il riferimento è il [codice IPA](https://www.indicepa.gov.it/ipa-portale/)[^1].
- **Niente ripetizioni nei valori.** Se la colonna si chiama `comune`, le celle non devono ripetere le parole «Comune di».
- **Dove trovare i codici.** La pagina [Codici e classificazioni](Tassonomie_elenchi_codici.md) raccoglie classificazioni e standard riutilizzabili.

[^1]: Indice dei domicili digitali delle pubbliche amministrazioni, dei gestori di pubblici servizi e delle società a controllo pubblico (Codice dell'amministrazione digitale, CAD, art. 6-ter)

## Come si fa nel foglio di calcolo

Excel toglie gli zeri iniziali quando apre un CSV, anche con l'importazione da Dati > Da testo/CSV (Data > From Text/CSV) se lasci il rilevamento predefinito: `082053` diventa `82053`. Prima di esportare, imposta le colonne di codici sul formato Testo; per aprire un CSV senza rovinarlo segui la procedura in [Esportare un CSV da Excel o LibreOffice](Linee_guida_importazione_esportazione.md#aprire-un-csv-in-excel-senza-rovinarlo).

Vedi anche: [7. Un solo tipo di dato per colonna](P07_tipi_dati.md), [8. Scrivi la stessa cosa sempre allo stesso modo](P08_standardizzazione_valori_campi.md), [Codici e classificazioni](Tassonomie_elenchi_codici.md).
