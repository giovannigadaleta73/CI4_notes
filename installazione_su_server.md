# INSTALLAZIONE SU SERVER

Dopo avere creato il dominio o sottodominio e attivato il protocollo https posso procedere ad installare una versione base di CI4 per poi sovrascrivere su questa il mio sito locale.

Su hosting (es. public_html\web)

- attivare le estensioni intl e mbstring e verifica la versione di php 

- installare CI4 da cPanel\Softacolous

Verifico che l’installazione sia andata a buon fine: carico la pagina principale web.piccoloweb.net e deve aprirsi la ‘wellcome page’ di CI4 notando che automaticamente il sito si sposta su  'Hello Bulma'

Il punto importante è che sono stati creati e configurati due file .htaccess e .env con le corrette impostazioni per far funzionare il sito. 

carico su hosting il sito che ho in locale cancellando le cartelle presenti e sostituendole con quelle che ho in locale. Mantengo invece i 2 file creati automaticamente.

- metto via le cartelle presenti (app, public…) inserendole in un archivio zip che userò in caso di ripristino e le elimino dalla root

- faccio upload delle sole cartelle che ho in locale e poi modifico il file [app\Config\App.php]:

        sostituendo 

```php
    public $baseURL = 'http://localhost:8080/';
```

        con 

```php
    public $baseURL = 'https://web.piccoloweb.net/public';  `
```

- Dopo avere creato il database su server, vado a impostare la relativa configurazione sul file `app\Config\Database.php`.
- Creo una migration

```shell
CLI> php spark make:migration CreateAnimals
```
