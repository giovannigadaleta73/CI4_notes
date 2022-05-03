# 6. Dati Model

Abbiamo visto le migration che sostituiscono le funzioni di un phpMyAdmin per la creazione di una tabella, adesso vediamo il model.

Una volta creato, il file presenta un elenco di proprietà suddivise in categorie.

Impostandole si attivano per per la propria tabella vincoli e comportamenti aggiuntivi.

Richiamando un'istanza del model nei Controller, avremo a disposizione un nuovo strumento per interagire col database. Sostituiremo il codice usato in precedenza con l'istanza del Model al fine di semplificare e potenziare la gestione dei dati, come:

+ connessione al db

+ operazioni CRUD (find, findAll...)

+ paginazione 

+ validazione dei dati
  
  [Link alle specifiche del Model]([Using CodeIgniter’s Model &mdash; CodeIgniter 4.1.9 documentation](https://codeigniter4.github.io/userguide/models/model.html#working-with-data))

Nei file Model troveremo proprietà suddivise nelle seguenti categorie:

+ Configurazione: nome della tabella da gestire e altre opzioni

+ Date: il Model crea e compila per noi le date di creazione, aggiornamento e cancellazione dei record. 

+ Validation: regole di validazione.
- Callbacks che possono essere richiamate prima e dopo le operazioni sulle tabelle (es. beforeInsert ).

Creo un model riferito ad una tabella: 

```shell
php spark make:model Libri
```

Il file creato sarà <mark>App\Models\Libri.php</mark>

!! N.B. CI4 crea automaticamente il nome della tabella mettendo al plurale, in inglese, il nome del model. Di conseguenza va corretto manualmente il nome della tabella. Es da libris a libri

```php
// viene creato automaticamente a partire dal comando CLI
protected $table            = 'libris';

// lo cambio in 
protected $table            = 'libri';
```

Una volta creato posso usare il model per le query. Vado a sostituire il precedente codice nel controller Catalogo:

```php
<?php

namespace App\Controllers;

use App\Controllers\BaseController;

class Catalogo extends BaseController
{
    public function index()
    {
        /*
        $db = \Config\Database::connect();

        $query = $db->query('SELECT * FROM libri');
        $dati['libri'] = $query->getResult();
        */

        $LibriModel = model('Libri');
/*
        $dati['libri'] = $LibriModel
            ->findAll();
*/
        $dati['libri'] = $LibriModel
            ->where('price <', 10)
            ->orderBy('id', 'ASC')
            ->findAll(10);

        return view('catalogo/index', $dati);
    }
}
```

Poichè i dati sono restituiti in forma di array, dobbiamo modificare nella view card.php le chiamate dei valori da oggetto ad array:

```php
// da
$libro->id 

// a
$libro['id']
```
