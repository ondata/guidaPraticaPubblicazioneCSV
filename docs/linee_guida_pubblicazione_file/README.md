# Linee guida per la pubblicazione di file CSV

La seguente sezione di questa guida fornisce linee guida sugli aspetti più comuni della preparazione dei dati tabellari per la pubblicazione come file `CSV`.

- P1-Singola fila di testi 
- P2-Singolo record per riga 
- P3-Nome delle colonne
- P4-Strutture di dati verticale vs. orizzontale
- P5-Trattamento dei valori sconosciuto
- P6-Subtotali, totali o raggruppamento
- P7-Tipi di dati 
- P8-Standardizzazione dei valori dei campi 
- P9-Campi codificati
- P10-Campi di testo
- P11-Campi numerici 
- P12-Campi con date
- P13-Campi con numeri di telefono
- P14-Campi con indirizzi postali
- P15-Campi con coordinate geografiche


## Singola linea di intestazione opzionale
Le tabelle di dati possono opzionalmente contenere una e una sola riga di intestazione per specificare i nomi dei campi.

Da prendere in considerazione:

• L'esistenza di più righe di intestazione, mentre possono aumentare l'interpretabilità dei dati per gli esseri umani a causa della loro espressività e formato, rendono difficile l'elaborazione per le macchine, quindi qualsiasi informazione aggiuntiva sui dati deve essere inclusa nella descrizione dei dati utilizzando i metadati appropriati nel Dizionario dei dati.
• I **nomi delle colonne** inclusi nella riga di intestazione sono un tipo di annotazione o metadati che descrivono ogni colonna e **non fanno parte dei dati**, cioè non dovrebbero essere considerati quando si conta il numero di righe di dati in una tabella.
• Per nominare le colonne si devono usare **celle singole** e in nessun caso celle unite.
• Si noti che non c'è alcun meccanismo per discernere automaticamente se il primo record in un CSV è una riga di intestazione, poiché è codificato come qualsiasi altro record. Pertanto, è buona pratica specificare la presenza o l'assenza di una riga di intestazione attraverso il dizionario dei dati includendo la proprietà "**`title`**".
• Un altro modo per indicare la presenza o l'assenza della linea di intestazione è un parametro content-type quando il file di dati è trasmesso via HTTP, della forma: **Content-Type: text/csv;header=absent**.

!!! example "Esempio 1: non usare celle multiple di intestazione"
    
    <kbd>cattiva prassi</kbd>
    
    | Dati sulle vendite di auto (anni 1998 - 1999) |
    | Unità espresse in migliaia |
    |----------------------------|
    | marchio | anno | vendite_per_anno |
    | ------- | ---- | ---------------- |
    | chevrolet chevelle malibu | 1998 | 2,50 |
    | chevrolet chevelle malibu | 1999 | 2,63 |
    | buick skylark 320 | 1998 | 3,40 |
    | buick skylark 320 | 1999 | 3,57 |
    
    <kbd>buona prassi</kbd>
    
    | marchio | anno | vendite_per_anno |
    |-------|----|----------------|
    | chevrolet chevelle malibu | 1998 | 2,50 |
    | chevrolet chevelle malibu | 1999 | 2,63 |
    | buick skylark 320 | 1998 | 3,40 |
    | buick skylark 320 | 1999 | 3,57 |
    
    
Le informazioni "Dati di vendita delle auto (anni 1998 - 1999)" e "Unità espresse in migliaia" dovrebbero essere trasferite al dizionario dei dati usando la proprietà "`description`".

!!! example "Esempio 2: non usare celle unite"

    <kbd>cattiva prassi</kbd>
    
    
    
    
    
    
    
    
    
