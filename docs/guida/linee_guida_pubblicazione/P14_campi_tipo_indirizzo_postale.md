---
hide:
- toc
# - navigation
title: Campi con indirizzi postali
---

# Campi con indirizzi postali

Utilizzare una codifica accurata degli indirizzi postali   essenziale per gestire le dimensioni geografiche con i dati. Indirizzi postali ben strutturati possono essere geolocalizzati, generando coordinate di latitudine e longitudine, utilizzando applicazioni specifiche.
  Da prendere in considerazione:
• Anche se esiste uno standard tecnico per laprogettazione dei record dei file discambio diinformazioni del registrocomunale(INE, Callejero de Censo Electoral),   consigliabile codificare un indirizzo postale come una stringa di caratteri con gli elementi necessari per localizzare un indirizzo all'interno di una localit .
• Questi elementi sono:
o tipo di strada (strada, viale, piazza, ...)
o nome della strada, numero, blocco, piano, lettera, ecc.
o localit  (nome)
o codice postale (5 caratteri numerici)
• Quando   possibile,   consigliabile utilizzare anche campi separati per i valori di latitudine e longitudine corrispondenti al punto geografico dell'indirizzo postale.


### Esempio:

codifica degli indirizzi postali in campi separati

!!! failure "Cattiva prassi"

    | marchio | indirizzo_rivenditore |
    | --- | --- |
    | chevrolet chevelle malibu | Viale Mazzini n° 23, Milano (20121) |
    | buick skylark 320 | Località Fabbre 33, Brera (20151) |
  
!!! success "Buona prassi"

    | marchio | rivenditore_tipo_via | rivenditore_indirizzo | rivenditore_civico | rivenditore_citta | rivenditore_cap |
    | --- | --- |
   | chevrolet chevelle malibu | Viale | Giuseppe Mazzini | 23 | Milano | 20121 |
   | buick skylark 320 | Località | Fabbre | 33 | Brera | 20151 |
   