---
hide:
- toc
# - navigation
title: Scrivi le coordinate in gradi decimali
---

# 15. Scrivi le coordinate in gradi decimali

Latitudine e longitudine devono essere in gradi decimali, con il punto, in due colonne separate chiamate `latitudine` e `longitudine`. Il sistema di riferimento deve essere dichiarato nel [dizionario dei dati](../dizionario_dati.md).

## Così sì e così no

Nomi delle biblioteche e coordinate di questa pagina sono inventati.

!!! failure "Così no"

    | biblioteca | latitudine | longitudine |
    | --- | --- | --- |
    | Biblioteca di esempio A | 38° 06' 56.52" | 13° 21' 41.40" |
    | Biblioteca di esempio B | 44° 55' 58.80" | 7° 32' 24.00" |
    | Biblioteca di esempio C | 45° 05' 42.00" | 10° 13' 22.80" |
    | Biblioteca di esempio D | 41° 53' 42.00" | 12° 29' 42.00" |

!!! success "Così sì"

    | biblioteca | latitudine | longitudine |
    | --- | ---: | ---: |
    | Biblioteca di esempio A | 38.1157 | 13.3615 |
    | Biblioteca di esempio B | 44.9330 | 7.5400 |
    | Biblioteca di esempio C | 45.0950 | 10.2230 |
    | Biblioteca di esempio D | 41.8950 | 12.4950 |

Le due tabelle indicano gli stessi punti: `38° 06' 56.52"` è uguale a 38 + 6/60 + 56.52/3600, cioè `38.1157`.

## Perché

Un programma di mappe disegna il punto leggendo due numeri. `38.1157` è un numero, `38° 06' 56.52"` è testo: chi riusa i dati deve prima convertirlo. In più il carattere `"` costringe a [mettere la cella tra virgolette](P10_campi_tipo_testo.md) e a raddoppiarlo.

## Casi particolari

### Sistema di riferimento

Gli stessi numeri, senza sistema dichiarato, sono ambigui, come una lunghezza senza unità di misura. Dichiara il sistema nel dizionario dei dati con il suo codice EPSG (European Petroleum Survey Group, l'organizzazione che ha creato il registro dei sistemi di riferimento). Se non sai quale sistema è stato usato, chiedilo a chi ha prodotto le coordinate.

Per le pubbliche amministrazioni italiane il sistema geodetico nazionale è ETRF2000, noto anche come RDN2008 (coordinate geografiche: EPSG:6706). Molte applicazioni web usano WGS84 (EPSG:4326): anche in questo caso va dichiarato.

### Ordine di longitudine e latitudine

Alcuni formati, come GeoJSON e il tipo `geopoint` di Table Schema, scrivono prima la longitudine e poi la latitudine. Con due colonne chiamate `latitudine` e `longitudine` l'ordine non crea dubbi.

### Altri casi

- **Più punti nella stessa riga**: aggiungi al nome il punto a cui si riferiscono, per esempio `sede_latitudine` e `sede_longitudine`.
- **Coordinate in altri formati**: si possono usare convertitori di coordinate UTM (Universal Transverse Mercator) o convertitori da gradi sessagesimali a gradi decimali[^1].
- **Linee e poligoni**: si può usare una colonna con la geometria in WKT (*Well-Known Text*, [OGC Simple Features](https://www.ogc.org/standards/sfa/)), per esempio `POLYGON((...))`, dichiarando il sistema di riferimento nel dizionario dei dati. Il WKT contiene virgole, quindi nel CSV la cella va tra virgolette.
- **Dati territoriali**: i metadati vanno documentati nel Repertorio nazionale dei dati territoriali (RNDT), come chiedono le [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-16).
- **Altri formati geografici**: se pubblichi dati puntuali in formati come GeoPackage, GeoJSON, [KML](https://it.wikipedia.org/wiki/Keyhole_Markup_Language) o [SHP](https://it.wikipedia.org/wiki/Shapefile), è consigliato affiancare un CSV con le coordinate, per facilitarne il riuso.

## Come si fa nel foglio di calcolo

Se hai gradi, primi e secondi in tre colonne, la formula è gradi + primi/60 + secondi/3600. Con i valori in `A2`, `B2` e `C2`: `=A2+B2/60+C2/3600`.

Prima di pubblicare, controlla in un editor di testo che i decimali abbiano il punto: vedi [Scrivi i numeri con il punto decimale](P11_campi_tipo_numerico.md).

[^1]: [Uno strumento per la conversione di coordinate](https://www.latlong.net/degrees-minutes-seconds-to-decimal-degrees)

Vedi anche: [10. Metti tra virgolette il testo che lo richiede](P10_campi_tipo_testo.md), [11. Scrivi i numeri con il punto decimale](P11_campi_tipo_numerico.md), [14. Dividi gli indirizzi in colonne](P14_campi_tipo_indirizzo_postale.md).
