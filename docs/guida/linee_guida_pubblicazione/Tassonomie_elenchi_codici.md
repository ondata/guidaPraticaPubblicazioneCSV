---
hide:
 - toc
# - navigation
title: Codici e classificazioni
---

Questa pagina raccoglie elenchi di codici e classificazioni da usare come valori delle colonne.

## Codici italiani

I codici sono sempre testo, non numeri: vanno pubblicati così come sono, zeri iniziali compresi. Nella tabella i valori di esempio sono quelli del Comune di Palermo; per il civico non ne riportiamo uno, perché non abbiamo verificato il valore nell'archivio.

| Codice | Identifica | Come si scrive | Esempio | Dove si trova |
| --- | --- | --- | --- | --- |
| Istat del comune | Il territorio del comune | 6 caratteri | `082053` | [SITUAS](https://situas.istat.it/web/) |
| Catastale | Il comune nel catasto | 4 caratteri | `G273` | [IndicePA](https://www.indicepa.gov.it/ipa-portale/) |
| IPA | L'amministrazione come ente | Testo | `c_g273` | [IndicePA](https://www.indicepa.gov.it/ipa-portale/) |
| Codice fiscale dell'ente | L'ente | 11 cifre, può iniziare per zero | `80016350821` | [IndicePA](https://www.indicepa.gov.it/ipa-portale/) |
| Ateco 2025 | L'attività economica | Con i punti | `47.81` | [Istat](https://www.istat.it/classificazione/ateco-2025/) |
| Numero civico | Il civico | Progressivo nazionale | Non indicato | [ANNCSU](https://www.anncsu.gov.it/it/consultazione-dellarchivio/open-data/) |

Il codice fiscale di una persona è un [dato personale](Dati_personali.md).

I codici cambiano nel tempo. Fusioni e riforme territoriali modificano l'elenco: dal 1° gennaio 2026 tutti gli enti locali della Sardegna hanno un codice nuovo (Cagliari è passata da `092009` a `118006`, Sassari da `090064` a `112050`), e dal 21 febbraio 2026 i comuni sono 7.894. Indica nel dizionario dei dati la data dei codici usati. L'elenco aggiornato è sulla [pagina Istat dei codici](https://www.istat.it/classificazione/codici-dei-comuni-delle-province-e-delle-regioni/), e SITUAS permette di interrogarli alla data desiderata.

### Per chi usa il terminale

[`opensituas`](https://pypi.org/project/opensituas/) scarica i codici da SITUAS e mostra la storia di un comune:

```
uv tool install opensituas
opensituas -o csv get 61 --out comuni.csv
opensituas cerca-codice comune Cagliari
```

Il primo comando produce l'elenco dei comuni, con il codice Istat nella colonna `PRO_COM_T`. Per i dati di IndicePA c'è `openipa-pp-cli`, che richiede un codice di accesso gratuito da chiedere al portale.

## Altri riferimenti

- [Classificazioni armonizzate a livello nazionale e internazionale Istat](https://www.istat.it/it/metodi-e-strumenti/classificazioni)
- [Thesaurus multilingue dell'Unione europea (EuroVoc)](https://eur-lex.europa.eu/browse/eurovoc.html?locale=it)
- [Nomenclatura delle attività economiche (NACE)](https://ec.europa.eu/eurostat/statistics-explained/index.php?title=NACE_background)
- [Nomenclatura delle unità territoriali per la statistica (NUTS)](https://ec.europa.eu/eurostat/web/nuts)
- [ISO 639-2, codici di lingua](http://www.loc.gov/standards/iso639-2/php/code_list.php)
- [ISO 4217, codici di valuta](https://www.iso.org/iso-4217-currency-codes.html)
- [ISO 3166-1, codici dei Paesi](https://www.iso.org/iso-3166-country-codes.html)
- [Unità di misura UN / UN/CEFACT](https://unece.org/fileadmin/DAM/cefact/recommendations/rec20/rec20_rev3_Annex3e.pdf)
- [Ontologie e vocabolari controllati AgID](https://github.com/italia/dati-semantic-assets)
- Catalogo nazionale della semantica dei dati, indicato dalle [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/capitolo-5.html#sec-arricchimento)
- [Tabelle di riferimento di EU Vocabularies](https://op.europa.eu/en/web/eu-vocabularies/authority-tables)

