# 1. INSTALLAZIONE

## installare php

+ installando xampp o simili verrà installato php e mysql
  + verifica: `php -v`
  + in <mark>php.ini</mark> abilitare:  `extension=intl`
  + avvieremo xampp in seguito quando dovremo collegarci al database
+ il percorso d'installazione di <mark>php.exe</mark> servirà per l'installazione di Composer

## installare composer

+ [Composer](https://getcomposer.org/download/)
  + verifica: `composer -v`

creazione di un progetto

il comando creerà una cartella contenente tutto il progetto

```shell
composer create-project codeigniter4/appstarter my-project
```

Il nostro progetto vuoto può essere avviato con il comando:

```shell
php spark serve
```

e come indicato nelle note sarà raggiungibile all'indirizzo http://localhost:8080

## creazione utente database

avvio il server Apache e il server Mysql di xampp poi scelgo Mysql / Admin che farà aprire phpMyAdmin

scelgo `Server:127.0.0.1`e la tab `Account Utente` e `Aggiungi Account Utente`

+ una opzione comoda è: `Crea un database con lo stesso nome e concedi tutti i privilegi`

Al termine avremo 

+ Utente: libreria, 

+ Pw: ****  

+ Db: libreria (il db prende lo stesso nome dell'utente)

Configurarazione base .env

Prima di iniziare a programmare, conviene abilitare la modalità di sviluppo. Questo ci permette di usare ad esempio la funzione `d()` che mostra la struttura degli elementi che le vengono passati come argomento. 

In oltrre compare una console a piè pagina con diverse informazioni.

modifico il file env ==> <mark>.env</mark>

e al suo interno cambio la riga Enviroment:

```php
#----------------------------------------------------------
# ENVIRONMENT
#----------------------------------------------------------

 CI_ENVIRONMENT = development
```

## configurazione per il database

Configuro il file <mark>App\Config\Database.php</mark> con

- utente

- pw

- nome del database

- nome host

- porta e altro.

Sullo stesso file posso preparare la configurazione che userò on line e lasciarla disattivata commentando la sezione. In alternativa, considerando che le impostazioni sul file <mark>Database.php</mark> vengono sovrascritte da quelle indicate nel file <mark>.env</mark> posso indicare sul file Database.php i dati per l’hosting e usare il file .env per la configurazione in locale (basterà poi escludere dal deploy il solo file .env) 

esempio file Database su server

```php
public $default = [
    'DSN' => '',
    'hostname' => 'mysql1001.mochahost.com',
    'username' => 'giovan12_libreria',
    'password' => 'password__libreriaAdmin',
    'database' => 'giovan12_libreria',
    //…
    'compress' => false,
    'strictOn' => false,
    'failover' => [],
    'port'     => 3306,
    ];
```

esempio file .env

```php
#--------------------------------------------------------------------
# DATABASE
#--------------------------------------------------------------------

 database.default.hostname = localhost
 database.default.database = libreria
 database.default.username = libreria
 database.default.password = password__libreriaAdmin
 database.default.DBDriver = MySQLi
# database.default.DBPrefix =
```
