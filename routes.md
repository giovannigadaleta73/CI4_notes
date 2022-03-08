# Routes

Possiamo iniziare a dare dei comandi alla nostra applicazione nel modo più semplice, digitandoli nell'url del browser seguendo questo schema di base:

        [ <span style="font-weight:bold">url sito internet</span> ]        [ <span style="font-weight:bold">comando</span> ]        [ <span style="font-weight:bold">eventuale parametro</span> ]

CI4 sfrutta il carattere / (slash) per identificare le parti l'url.

<span style="color: #393; font-weight:bold">url sito internet</span>

La prima parte rappresenta l'indirizzo internet del sito su cui ci troviamo e viene riconosciuta da CI4 perché questo indirizzo é impostato nella variabile di configurazione *<u><strong>$baseURL</strong></u>* che troviamo in `app\Config\App.php`.

> A seconda delle configurazioni si potrà presentare anche *<u><strong>index.php</strong></u>* all'interno dell'url.

- on line avrò qualcosa di simile a questo:
  
  ```url
  https://mio.sito.com
  ```

- in locale posso trovare questo
  
  ```url
  http://localhost:8080
  oppure
  http://localhost:8080/index.php
  ```



<span style="color: #393; font-weight:bold">comando</span>

Qui siamo al punto principale: con il comando indichiamo quale azione eseguire alla nostra applicazione. 

Il comando si compone di due parti separate del carattere /

```
controller / metodo
```

In tal modo scrivendo un url come questa:

```php
mio.sito.com/prodotti/elenco
```

 CI4 cercherà un controller con il nome ***<u>Prodotti</u>*** e al suo interno il metodo ***<u>elenco</u>***.

Ci sono a questo punto due considerazioni da fare:

1. Se la mia url si ferma al controller 
   
   ```php
   mio-sito.com/prodotti
   ```
   
   CI4 cercherà automaticamente il metodo ***<u>index</u>***

2. Se scrivo qualsiasi cosa dopo il controller ***<u>prodotti / </u>*** CI4 lo considererà come nome del metodo da cercare. Questo significa che come impostazione standard non protrò scrivere 
   
   ```php
   mio-sito.com/prodotti/12
   ```
   
   poichè 12 non sarà interpretato come parametro del metodo index, ma verrà visto come nome di un metodo da cercare nel controller Prodotti.php

<span style="color: #393; font-weight:bold">parametro</span> 

Se l'url contiene il controller e il metodo allora posso inserire uno o più parametri sempre separati dal carattere slash(/). Se il metodo riceve meno parametri di quelli richiesti, verrà segnalato un errore. 

Quindi se il metodo ***<u>calcola</u>*** che richiete tre parametri:

```php
class Esercizi extends BaseController
    {
        public function calcola($somma1, $somma2, $somma3)
            { ...
```

la mia url dovrà essere qualcosa di simile a questo:

```php
www.mio.sito.com/esercizi/calcolatotale/20/30/10
```

 Per non ricevere un messaggio di errore nel caso l'url contenga meno parametri di quelli richiesti, basterà impostare nel metodo calcolaTotale dei velori di default:

```php
public function calcola($somma1 = 10, $somma2 = 300, $somma3 = null)
    { ...
```

#### I placeholder

Questo comportamento standard 

        [ **url sito internet** ]        [ **comando** ]        [ **eventuale parametro** ]

si può semplificare: il ***<u>comando</u>*** scritto nell'url si può sostituire con un ***<u>nome</u>***, passando da questa situazione

```php
mio-sito/prodotti/modifica/12
```

a questa

```
mio-sito/elabora/12
```

Per ottenere questo risultato si vanno a create delle ***<u>routes</u>*** nel file `app\Config\Routes.php` 

```php
$routes->get('/modifica/(:num)', 'Products::edit/$1')
```

Nell'esempio il secondo segmento del nome della route rappresenta il parametro che passiamo al nostro metodo.

#### Tipi di parametro

Una premessa: se il segmento dedicato al parametro è previsto nel nome della route

```php
... $routes->get('/modifica/(:num)', ...
```

allora dovrà essere presente altrimenti CI4 restituirà il messaggio di pagina non trovata.

CI4 permette di restringere il tipo di dati che può essere accettato. Partiamo dalla categoria più ampia scendendo man mano nelle categorie che impongono maggiori restrizioni ai tipi di caratteri consentiti. In tutte le tipologie di placeholder elencate il simbolo slash / viene riconosciuto solo come termine di un segmento

- (:any)                accetta ogni tipo di carattere (alfanumerici e simboli) se compaiono più parametri (separati dallo slash / questi verranno tutti inviati alla funzione indicata)

- (:segment)       accetta ogni tipo di carattere (alfanumerici e simboli) se compaiono più parametri (separati dallo slash /) verranno inviati tanti parametri quante volte compare (:segment). 
  
  ```php
  ...
  $routes->get('/modifica/(:segment)/(:segment)', 
  ... 
  invia i primi 2 parametri incontrati
  ```

- (:hash)        equivalente a (:segment) usato per identificare le route con hash

- (:alpha)       solo caratteri alfabetici senza simboli        

- (:num)         solo numeri senza simboli

- (:alphanum)    caratteri alfanumerici senza simboli

Si possono impostare delle combinazioni
