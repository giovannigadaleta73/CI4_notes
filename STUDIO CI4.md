# CI4

### Installazione in locale

Installo un server locale come xampp avvio il servizio database e creo il mio DB. In CI4 configuro l'applicazione in modo che possa interfacciarsi con questo. Le tabello posso crearle manualmente tramite phpMyAdmin oppure tramite le <u>*migration*</u> con il vantaggio di standardizzare la procedura e di poterla replicare in pochi secondi in caso di necessità durante le fasi di sviluppo. Le tabelle verranno popolate con il <u>*seeder*</u>, una comoda libreria che genera dei contenuti placeholder.

Per impartire dei comandi all'applicazione si sfrutta l'url. La struttura  tipica [[w]]([URI Routing &mdash; CodeIgniter 4.1.9 documentation](https://codeigniter4.github.io/userguide/incoming/routing.html#setting-your-own-routing-rules)) si presenta così: 

```
sito.com/controller/metodo/parametro/
```

controller è una classe (che coincide anche con il nome del file php) che contiene i metodi che possono essere richiamati indicandoli come secondo componente dell'url.

Il terzo componente comprende gli eventuali parametri da passare al metodo.

Con questa chiamata la nostra applicazione esegue delle istruzioni e queste possono restituire o meno un risultato: 

- svolge delle istruzioni ma non restituisce un risultato

- restituisce un risultato in forma di dati che verranno usati da un altro programma

- come risultato viene chiamata una view a cui sono passati degli eventuali dati

Le view sono le pagine web del nostro sito. Tutto quello che appare a video è il risultato della elaborazione delle view. Possono mostrare i dati che passati dal controller, come risultato della consultazione di un database, oppure contenere un form o qualsiasi altro tipo di pagina. Le pagine che vediamo possono essere il risultato di singoli file oppure devirano dell'aggregazione di più componenti (header, body, footer...).

Il controller può gestire dei dati provenienti da una o più tabelle del nostro database. Le tabelle non sono però gestite in maniera diretta dal controller, ma tramite i file di model. Ogni tabella ha un suo model (un file php che contiene una classe omonima). CI4 ha una classe model che mette a disposizione dei model che creiamo noi, una serie di comandi standard, semplificando la gestione del db.

Per usare un db è necessario scricare un comune server locale come xampp e avviare i servizi apache e sql. Creiamo manualmente il DB (con phpMyAdmin o tool simili compresi già nel server locale che scegliamo). Quindi creiamo una utenza e la colleghiamo a questo. Poi dovremo passare a CI4 i dati per potersi connettere.

A questo punto creiamo le nostre tabelle tramite le <u>*migration*</u> e, se necessario, le popoliamo tramite i seeder per la fase di sviluppo. I file delle migration in locale possono essere richiamati da CLI con i comandi della libreria spark, oppure creando delle apposite routes. Su server invece avrò solo quest'ultima possibilità non potendo avere a disposizione la CLI.



github

i comandi per avviare il server

riepilogo su <u>*spark*</u> [online](https://onlinewebtutorblog.com/complete-codeigniter-4-spark-cli-tutorial/)

controller, route e view iniziali

controller

view

### Installazione su server

Per spostare il nostro sito on line dovremo creare un eventuale sottodominio, impostare la versione corretta di Php e abilitare le estensioni richieste da CI4. 

Se è possibile usiamo Softacolous per installare CI4 nel dominio o sottodominio. Questo passaggio serve perchè verranno creati automaticamente dal sistema i file .htaccess e App.php con le corrette impostazioni. Sostituiremo tutto il resto con il nostro progetto con un normale copia e incolla delle cartelle in locale. 

Il database può essere creato durante la fase di installazione tramite Softacolous altrimenti lo creeremo noi da cPanel, creeremo poi un'utenza da collegare al DB. 

In questo momento il DB non ha tabelle. Queste posso importarle dal db locale o con le migration e poi i seeder. Su server non ho modo di lanciare i comandi dalla CLI di conseguenza tali comandi dovranno avere delle loro routes configurate appositamente, mentre i file delle migration dovrò caricarli da locale con tutto il progetto.

```php
$routes->cli('migrate', 'App\Database::migrate');
```

Creare il DB e l'utenza

le tabelle e i dati si importano
