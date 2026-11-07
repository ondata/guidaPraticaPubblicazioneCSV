---
hide:
 - toc
# - navigation
---

# Campi con coordinate geografiche

Il formato più usato per rappresentare le **coordinate geografiche** sulle **mappe** è:

  - la **latitudine** e la **longitudine** in **gradi decimali**, i cui valori dovrebbero essere presentati in **colonne separate**, con intestazioni di colonna da nominare: latitudine e longitudine, rispettivamente.

Da prendere in considerazione:

  - se è necessario specificare il **nome di un'entità** di cui si riportano le **coordinate**, si usano i **suffissi** "\_latitudine" e "\_longitudine";
  - si possono usare convertitori di coordinate UTM o convertitori da gradi sessagesimali a gradi decimali[^1];
  - per i **dati geografici diversi dai punti**, ad esempio linee o poligoni, si può usare una colonna con la geometria in **WKT** (*Well-Known Text*, [OGC Simple Features](https://www.ogc.org/standards/sfa/)), ad esempio `POLYGON((...))`, dichiarando il sistema di riferimento nel dizionario dei dati.

È consigliabile, per facilitare il loro riutilizzo, ogni volta che si pubblicano dati geografici puntuali in formati come [SHP](https://it.wikipedia.org/wiki/Shapefile) o [KML](https://it.wikipedia.org/wiki/Keyhole_Markup_Language), accompagnare questi file con un file CSV in cui sono incluse le coordinate geografiche.

[^1]: [Uno strumento per la conversione di coordinate](https://www.latlong.net/degrees-minutes-seconds-to-decimal-degrees)

### Esempio:
coordinate in gradi decimali, in due colonne.

!!! failure "Cattiva prassi"


    | rivenditore | latitudine  | longitudine |
    | ----------- | ----------- | ----------- |
    | chevrolet   | 43° 14' 04" | 5° 04' 24"  |
    | buick       | 43° 20' 44" | 5° 14' 14"  |


!!! success "Buona prassi"

    | rivenditore | latitudine | longitudine |
    | ----------- | ---------: | ----------: |
    | chevrolet   | 43.2344444 | 5.07333333  |
    | buick       | 43.3455555 | 5.23722222  |
