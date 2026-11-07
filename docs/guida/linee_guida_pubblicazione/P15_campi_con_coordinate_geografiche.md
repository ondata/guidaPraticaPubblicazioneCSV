---
hide:
 - toc
# - navigation
---

# Campi con coordinate geografiche

Il formato più usato per rappresentare le **coordinate geografiche** sulle **mappe** è:

  - la **latitudine** e la **longitudine** in **gradi decimali**, i cui valori dovrebbero essere presentati in **colonne separate**, con intestazioni di colonna da nominare: latitudine e longitudine, rispettivamente.

Dichiara sempre il **sistema di riferimento** nel dizionario dei dati, con il suo codice EPSG: gli stessi numeri, senza sistema dichiarato, sono ambigui. Per le pubbliche amministrazioni italiane il sistema geodetico nazionale è ETRF2000, noto anche come RDN2008 (coordinate geografiche: EPSG:6706). Molte applicazioni web usano WGS84 (EPSG:4326): anche in questo caso va dichiarato. Rendi esplicito anche l'ordine con i nomi delle colonne: GeoJSON e il tipo `geopoint` di Table Schema usano longitudine, latitudine.

Se il dato è territoriale, i metadati vanno documentati nel Repertorio nazionale dei dati territoriali (RNDT), come chiedono le [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/capitolo-4.html#req-16).

Da prendere in considerazione:

  - se è necessario specificare il **nome di un'entità** di cui si riportano le **coordinate**, si usano i **suffissi** "\_latitudine" e "\_longitudine";
  - si possono usare convertitori di coordinate UTM o convertitori da gradi sessagesimali a gradi decimali[^1];
  - per i **dati geografici diversi dai punti**, ad esempio linee o poligoni, si può usare una colonna con la geometria in **WKT** (*Well-Known Text*, [OGC Simple Features](https://www.ogc.org/standards/sfa/)), ad esempio `POLYGON((...))`, dichiarando il sistema di riferimento nel dizionario dei dati.

È consigliabile, per facilitare il loro riutilizzo, ogni volta che si pubblicano dati geografici puntuali in formati come GeoPackage, GeoJSON, [KML](https://it.wikipedia.org/wiki/Keyhole_Markup_Language) o [SHP](https://it.wikipedia.org/wiki/Shapefile), accompagnare questi file con un file CSV in cui sono incluse le coordinate geografiche.

[^1]: [Uno strumento per la conversione di coordinate](https://www.latlong.net/degrees-minutes-seconds-to-decimal-degrees)

### Esempio:
coordinate in gradi decimali, in due colonne.

!!! failure "Cattiva prassi"


    | rivenditore | latitudine  | longitudine |
    | ----------- | ----------- | ----------- |
    | chevrolet   | 38° 07' 00" | 13° 21' 40" |
    | buick       | 45° 28' 00" | 9° 11' 24"  |


!!! success "Buona prassi"

    | rivenditore | latitudine | longitudine |
    | ----------- | ---------: | ----------: |
    | chevrolet   | 38.116667  | 13.361111   |
    | buick       | 45.466667  | 9.190000    |
