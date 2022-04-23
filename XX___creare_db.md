# I DATI

In locale uso le migration e i seed per ricreare la struttura delle tabelle e i dati per i test, poi con un esporta/importa le riporto sull’ hosting (non ho modo di lanciare le migration sull’hosting).

```shell
CLI> php spark migrate
```

```shell
CLI> php spark db:seed PopulateProducts
```

*[1]*

[**LOCALE**] Vado in phpMyAdmin `Server: 127.0.0.1 / Account Utenti` nella maschera per creare un nuovo utente e fleggo l’opzione [crea db con lo stesso nome]

[**HOSTING**] `cPanel \ Databases \ MySql Databases` Creo un utente e poi lo associo ad un database

*[2]
