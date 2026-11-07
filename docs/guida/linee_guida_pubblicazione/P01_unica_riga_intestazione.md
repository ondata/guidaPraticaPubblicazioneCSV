---
hide:
 - toc
# - navigation
title: Una sola riga di intestazione
---

Il file contiene sempre una, e una sola, riga di intestazione, nella prima riga. Il formato CSV ammette anche file senza intestazione (RFC 4180), ma chi pubblica dati non dovrebbe usare questa possibilità: lo raccomandano anche le [Linee guida AgID](https://ondata.github.io/linee-guida-opendata/allegato-B.html#csv).

Da prendere in considerazione:

- L'esistenza di più righe di intestazione, mentre possono aumentare l'interpretabilità dei dati per gli esseri umani a causa della loro espressività e formato, rendono difficile l'elaborazione per le macchine, quindi qualsiasi informazione aggiuntiva sui dati deve essere inclusa nella descrizione dei dati utilizzando i metadati appropriati nel dizionario dei dati.

- I **nomi delle colonne** inclusi nella riga di intestazione sono un tipo di annotazione o metadati che descrivono ogni colonna e **non fanno parte dei dati**, cioè non dovrebbero essere considerati quando si conta il numero di righe di dati in una tabella.

- Per nominare le colonne si devono usare **celle singole** e in nessun caso celle unite.

- Per i file ereditati senza intestazione, l'assenza va dichiarata: in CSVW con `"dialect": {"header": false}`, in Table Dialect con `"header": false`, oppure via HTTP con `Content-Type: text/csv;header=absent`. Nessun programma può capirlo da solo, perché la prima riga è codificata come qualsiasi altra.


### Esempio 1:
non usare celle multiple di intestazione.

!!! failure "Cattiva prassi"

    <table class="tabella">
    	<tbody>
    		<tr class="arancione_grassetto">
    			<td rowspan="1" colspan="3">Dati sulle vendite di auto (anni 1998 - 1999)</td>
    		</tr>
    		<tr class="arancione_grassetto">
    			<td rowspan="1" colspan="3">Unit&agrave; espresse in migliaia</td>
    		</tr>
    		<tr class="arancione_grassetto">
    			<td>marca</td>
    			<td>anno</td>
    			<td>vendite_per_anno</td>
    		</tr>
    		<tr>
    			<td>chevrolet chevelle malibu</td>
    			<td>1998</td>
    			<td>2.5</td>
    		</tr>
    		<tr>
    			<td>chevrolet chevelle malibu</td>
    			<td>1999</td>
    			<td>2.63</td>
    		</tr>
    		<tr>
    			<td>buick skylark 320</td>
    			<td>1998</td>
    			<td>3.4</td>
    		</tr>
    		<tr>
    			<td>buick skylark 320</td>
    			<td>1999</td>
    			<td>3.57</td>
    		</tr>
    	</tbody>
    </table>

!!! success "Buona prassi"

    <table xmlns="http://www.w3.org/1999/xhtml" class="tabella">
    	<tbody>
    		<tr class="arancione_grassetto">
    			<td>marca</td>
    			<td>anno</td>
    			<td>vendite_per_anno</td>
    		</tr>
    		<tr>
    			<td>chevrolet chevelle malibu</td>
    			<td>1998</td>
    			<td>2.5</td>
    		</tr>
    		<tr>
    			<td>chevrolet chevelle malibu</td>
    			<td>1999</td>
    			<td>2.63</td>
    		</tr>
    		<tr>
    			<td>buick skylark 320</td>
    			<td>1998</td>
    			<td>3.4</td>
    		</tr>
    		<tr>
    			<td>buick skylark 320</td>
    			<td>1999</td>
    			<td>3.57</td>
    		</tr>
    	</tbody>
    </table>



Le informazioni "Dati di vendita delle auto (anni 1998 - 1999)" e "Unità espresse in migliaia" dovrebbero essere trasferite al dizionario dei dati usando la proprietà "`dc:description`".

### Esempio 2:
non usare celle unite.

!!! failure "Cattiva prassi"

    <table xmlns="http://www.w3.org/1999/xhtml" class="tabella">
    	<tbody>
    		<tr class="arancione_grassetto">
    			<td rowspan="2" colspan="1">marca</td>
    			<td rowspan="1" colspan="2">contatto_concessionario</td>
    		</tr>
    		<tr class="arancione_grassetto">
    			<td>concessionario_mail</td>
    			<td>concessionario_telefono</td>
    		</tr>
    		<tr>
    			<td>chevrolet chevelle malibu</td>
    			<td>mail@concessionario_chevrolet.com</td>
    			<td>+39-1111111</td>
    		</tr>
    		<tr>
    			<td>buick skylark 320</td>
    			<td>mail@concessionario_buick.com</td>
    			<td>+39-2222222</td>
    		</tr>
    	</tbody>
    </table>


!!! success "Buona prassi"

    <table xmlns="http://www.w3.org/1999/xhtml" class="tabella">
    	<tbody>
    		<tr class="arancione_grassetto">
    			<td>marca</td>
    			<td>contatto_concessionario_mail</td>
    			<td>contatto_concessionario_telefono</td>
    		</tr>
    		<tr>
    			<td>chevrolet chevelle malibu</td>
    			<td>mail@concessionario_chevrolet.com</td>
    			<td>+39-1111111</td>
    		</tr>
    		<tr>
    			<td>buick skylark 320</td>
    			<td>mail@concessionario_buick.com</td>
    			<td>+39-2222222</td>
    		</tr>
    	</tbody>
    </table>
