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
    
    <style>
    .cell1 { background-color: #ffffff; color: #000000; font-family: Arial; font-size: 10pt; font-style: normal; font-weight: bold; text-align: center; vertical-align: bottom;   border-left-style: solid; border-left-width: 1px; border-left-color: #666666 border-right-style: solid; border-right-width: 1px; border-right-color: #666666 border-top-style: solid; border-top-width: 1px; border-top-color: #666666 border-bottom-style: solid; border-bottom-width: 1px; border-bottom-color: #666666 }
.cell2 { background-color: #ffffff; color: #24292f; font-family: Arial; font-size: 10pt; font-style: normal; font-weight: bold; text-align: left; vertical-align: bottom; border-left-style: solid; border-left-width: 1px; border-left-color: #666666 border-right-style: solid; border-right-width: 1px; border-right-color: #666666 border-top-style: solid; border-top-width: 1px; border-top-color: #666666 border-bottom-style: solid; border-bottom-width: 1px; border-bottom-color: #666666 }
.cell3 { background-color: #ffffff; color: #000000; font-family: Arial; font-size: 10pt; font-style: normal; font-weight: bold; text-align: left; vertical-align: bottom; border-left-style: solid; border-left-width: 1px; border-left-color: #666666 border-right-style: solid; border-right-width: 1px; border-right-color: #666666 border-top-style: solid; border-top-width: 1px; border-top-color: #666666 border-bottom-style: solid; border-bottom-width: 1px; border-bottom-color: #666666 }
.cell4 { background-color: #ffffff; color: #000000; font-family: Arial; font-size: 10pt; font-style: normal; font-weight: normal; text-align: left; vertical-align: bottom; border-left-style: solid; border-left-width: 1px; border-left-color: #666666 border-right-style: solid; border-right-width: 1px; border-right-color: #666666 border-top-style: solid; border-top-width: 1px; border-top-color: #666666 border-bottom-style: solid; border-bottom-width: 1px; border-bottom-color: #666666 }
.cell5 { background-color: #ffffff; color: #24292f; font-family: Arial; font-size: 10pt; font-style: normal; font-weight: normal; text-align: left; vertical-align: bottom; border-left-style: solid; border-left-width: 1px; border-left-color: #666666 border-right-style: solid; border-right-width: 1px; border-right-color: #666666 border-top-style: solid; border-top-width: 1px; border-top-color: #666666 border-bottom-style: solid; border-bottom-width: 1px; border-bottom-color: #666666 }
.cell6 { background-color: #ffffff; color: #24292f; font-family: ui-monospace, SFMono-Regular, "SF Mono", Menlo, Consolas, "Liberation Mono", monospace; font-size: 10pt; font-style: normal; font-weight: normal; text-align: left; vertical-align: bottom; border-left-style: solid; border-left-width: 1px; border-left-color: #666666 border-right-style: solid; border-right-width: 1px; border-right-color: #666666 border-top-style: solid; border-top-width: 1px; border-top-color: #666666 border-bottom-style: solid; border-bottom-width: 1px; border-bottom-color: #666666 }
    </style>

    <table style="border-collapse: collapse;">
    <colgroup>
       <col width="169" />
      <col width="104" />
      <col width="133" />
    </colgroup>
    <tr height="21"><td colspan=3 class="cell1">Dati sulle vendite di auto (anni 1998 - 1999)</td></tr>
    <tr height="21"><td colspan=3 class="cell1">Unità espresse in migliaia</td></tr>
    <tr height="21"><td class="cell2">marchio </td><td class="cell3">anno</td><td class="cell3">vendite_per_anno</td></tr>
    <tr height="21"><td class="cell4">chevrolet chevelle malibu</td><td class="cell4">1998</td><td class="cell4">2,50</td></tr>
    <tr height="21"><td class="cell5">chevrolet chevelle malibu  </td><td class="cell4">1999</td><td class="cell4">2,63</td></tr>
    <tr height="21"><td class="cell4">buick skylark 320</td><td class="cell4">1998</td><td class="cell4">3,40</td></tr>
    <tr height="21"><td class="cell6">buick skylark 320</td><td class="cell4">1999</td><td class="cell4">3,57</td></tr>
    </table>
    
    <kbd>buona prassi</kbd>
    
    | marchio | anno | vendite_per_anno |
    | ------- | ---- | ---------------- |
    | chevrolet chevelle malibu | 1998 | 2,50 |
    | chevrolet chevelle malibu | 1999 | 2,63 |
    | buick skylark 320 | 1998 | 3,40 |
    | buick skylark 320 | 1999 | 3,57 |
    
    
    
Le informazioni "Dati di vendita delle auto (anni 1998 - 1999)" e "Unità espresse in migliaia" dovrebbero essere trasferite al dizionario dei dati usando la proprietà "`description`".

!!! example "Esempio 2: non usare celle unite"

    <kbd>cattiva prassi</kbd>
    
    
    
    
    
    
    
    
    
