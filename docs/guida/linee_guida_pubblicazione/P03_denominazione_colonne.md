




# Denominazione delle colonne

I nomi dei campi o delle colonne in una tabella di dati devono essere comprensibili alle persone.

Da prendere in considerazione:

- In molti casi, le colonne delle tabelle di dati mantengono i nomi assegnati dai sistemi di gestione di database, di solito soggetti a convenzioni tecniche che sono difficili da capire per le persone.
- Alcune raccomandazioni per la nomina dei campi:
   - Non ripetere i nomi dei campi.
   - Usate nomi brevi (nell'ordine di 20 caratteri) ma tenendo sempre presente che il risparmio di caratteri non deve portare a un'errata interpretazione del nome del campo. 
   - Evitare di usare abbreviazioni.
   - Usa solo caratteri ASCII minuscoli (a-z; 0-9)
   - Non usare caratteri speciali (per esempio äüöàéèê, ecc.).
   - Non includere accenti o segni di punteggiatura.
   - Usate i trattini bassi "`_`" per separare le parole che compongono i nomi delle colonne invece degli spazi bianchi.
   - Evitare l'uso di codici, e se assolutamente necessario, dovrebbe essere completamente spiegato nel dizionario dei dati che documenta il set di dati.
   - I nomi dei campi devono corrispondere a quelli specificati nel dizionario dei dati.

**Esempio**: denominazione comprensibile delle colonne

|Identificatore_M|Annio|Cil.|Consumo_per_100_k ms_di_viaggio_urbano|HP|m/sec^2|
|---|---|---|---|----|----|
|chevrolet chevelle malibu|1970|8|18|130|12|
|buick skylark 320|1970|8|15|165|11,5|
|plymouth satellite|1970|8|18||150|11|


|marchio|anno|cilindri|consumo|potenza|accelerazione|
|---|---|---|---|----|----|
|chevrolet chevelle malibu|1970|8|18|130|12|
|buick skylark 320|1970|8|15|165|11,5|
|plymouth satellite|1970|8|18|150|11|

Se c'è un'entità che comprende diverse caratteristiche separate in diversi campi, è conveniente iniziare a nominare i campi con quell'entità e poi con gli attributi più specifici (dal più generale al più specifico). Per esempio:

|nome_cliente|addebito al cliente|tipo di documento del richiedente|numero del documento del richiedente|
|---|---|---|---|
| |  |  |  |

I campi che sono identificatori possono includere il suffisso "`_id`" nel nome del campo, tranne in casi eccezionali in cui un nome alternativo è più conveniente perché fornisce informazioni sul sistema di identificazione usato.

Per i campi che contengono la descrizione di quell'identificatore, si raccomanda di includere il suffisso "`_name`", a meno che non ci sia un modo più conveniente per nominare il campo.

|dealer_id|nome_concessionario|
|---|---|
|   |   |

