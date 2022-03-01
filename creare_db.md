## - - CREARE IL DB

Sia che abbia già delle migration pronte in un progetto da clonare in locale, sia che le debba creare da zero, creo il database vuoto con l’utenza [1] (stessa cosa faccio sul mio hosting per il successivo deploy).

Configuro [App\Config\Database.php] [2] con utente, pw, nome del database, nome host, porta e altro. Sullo stesso file posso preparare la configurazione che userò on line e lasciarla disattivata commentando la sezione. In alternativa posso indicare  su file i dati per l’hosting [3] e usare .env per la configurazione in locale (basterà poi escludere dal deploy il solo file .env) 

Creo una configurazione per il mio sito in locale, poi ne preparo una sull’hosting. In tal modo, mentre la configurazione si adatta ad ogni deploy, il codice del progetto non cambia e posso rapidamente tenerlo sincronizzato.

Le impostazioni sul file [Database.php] vengono sovrascritte da quelle indicate nel file [.env]

In locale uso le migration e i seed per ricreare la struttura delle tabelle e i dati per i test, poi con un esporta/importa le riporto sull’ hosting (non ho modo di lanciare le migration sull’hosting).

CLI> php spark migrate

CLI> php spark db:seed PopulateProducts

[1]

[LOCALE] Vado in phpMyAdmin [[Server: 127.0.0.1](http://localhost/phpmyadmin/index.php?route=/) / Account Utenti] nella maschera per creare un nuovo utente e fleggo l’opzione [crea db con lo stesso nome]

[HOSTING] cPanel \ Databases \ MySql Databases Creo un utente e poi lo associo ad un database

[2]

public $default = [

'DSN'      => '',

         'hostname' => 'localhost',

         'username' => 'giovan12_game_store',

         'password' => 'codeigniter_1',

         'database' => 'giovan12_game_store',

…

     'compress' => false,

     'strictOn' => false,

     'failover' => [],

     'port'     => 3306,

];

[3]

public $default = [

        'DSN'      => '',

        'hostname' => 'mysql1001.mochahost.com',

        'username' => 'giovan12_game_store',

        'password' => 'codeigniter_1',

        'database' => 'giovan12_game_store',

…

        'compress' => false,

        'strictOn' => false,

        'failover' => [],

        'port'     => 3306,

];
