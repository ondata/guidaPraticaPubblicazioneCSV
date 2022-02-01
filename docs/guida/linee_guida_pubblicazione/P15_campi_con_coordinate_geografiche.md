---
hide:
 - toc
# - navigation
---

Il formato più usato per rappresentare le coordinate geografiche sulle mappe è:

  - la latitudine e la longitudine in gradi decimali, i cui valori dovrebbero essere presentati in colonne separate, con intestazioni di colonna da nominare: Latitudine e Longitudine, rispettivamente.

Da prendere in considerazione:

  - Se è necessario specificare il nome di un'entità di cui si riportano le coordinate, si usano i suffissi "\_latitudine" e "\_longitudine".
  - Si possono usare convertitori di coordinate UTM o convertitori gradi sessagesimali a gradi decimali [qui uno strumento per conversione](http://www.geoin.it/coordinate_converter/).
  - Per i dati geografici diversi dai punti, ad esempio linee o poligoni, si raccomanda di seguire la specifica *Well-knowntext representations of coordinate reference systems* (WKT-CRS) dell'[Open Geospatial Consortium](https://www.opengeospatial.org/standards/wkt-crs).

È consigliabile, ogni volta che si pubblicano dati geografici in formati come [SHP](https://es.wikipedia.org/wiki/Shapefile) o [KML](https://es.wikipedia.org/wiki/KML), accompagnare questi file con un file CSV in cui sono incluse anche le coordinate geografiche per facilitare il loro riutilizzo.

**Esempio**: uso di campi codificati

!!! failure "Cattiva prassi"


    | rivenditore | latitudine  | longitudine |
    | ----------- | ----------- | ----------- |
    | chevrolet   | 43° 14' 04" | 5° 04' 24"  |
    | buick       | 43° 20' 44" | 5° 14' 14"  |


!!! success "Buona prassi"

    | rivenditore | latitudine | longitudine |
    | ----------- | ---------: | ----------: |
    | chevrolet   | 43.2345678 | -5.1234567  |
    | buick       | 43.3456789 | -5.2345678  |
