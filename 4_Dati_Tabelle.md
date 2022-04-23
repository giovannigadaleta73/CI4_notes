# 4. DATI - CREARE LE TABELLE

Dopo aver configurato la connessione al database possiamo creare le sue tabelle. Anzichè procedere manualmente con phpMyAdmin, CI4 fornisce le migration: file che contengono istruzioni per creare e modificare le tabelle del nostro progetto. Sostituiscono e rendono rapide tutte quelle operazioni fatte manualmente con i vari programmi di gestione dei database come phpMyAdmin. Il nome della migration segue la notazione PascalCase.

```
CLI> php spark make:migration CreaLibreria
```

Con questo comando viene generata una classe con due metodi: up e down, per la creazione o modifica delle tabelle e il ripristino alla situazione iniziale.

In sequenza il metodo **up** conterrà:

+ campi `$this->forge->addField([ … ]);`

+ indice `$this->forge->addField('id');`

+ nome della tabella `$this->forge->createTable('animals');`

Mentre nel metodo **down** `$this->forge->dropTable('products');`

> per le specifiche: 
> 
> [Database Forge documentation](https://codeigniter4.github.io/userguide/dbmgmt/forge.html#adding-fields)

```php
public function up()
{
    $this->forge->addField([
        'id' =>  [
            'type' => 'INT',
            'constraint' => 11,
            'unsigned' => true,
            'auto_increment' => true,
            ],
        'titolo' => [
            'type' => 'VARCHAR',
            'constraint' => 255,
            'unique' => true,
            ],
        'incipit' => [
            'type' => 'TEXT',
            'null' => true,
            ],
        'price' => [
            'type' => 'DECIMAL',
            'constraint' => '10,2',
            ]
        ]);

    $this->forge->addKey('id');
    $this->forge->createTable('libri');
}

public function down()
{
    $this->forge->dropTable('libri');
}
```

Dopo averla creata si avvia con

```
CLI> php spark migrate
```

Con questo comando CI4 crea la tabella nel db. A questo punto possiamo inserire i dati. In fase di test possiamo importare dei dati già pronti o creare dei dati fittizzi con la libreria Faker. CI4 fornisce la libreria seeder per facilitare l'inserimento massivo di dati.

## Modifica di una tabella

Per apportare delle variazioni alle tabelle già create, uso sempre una migration. La nomino in modo significativo:

```shell
php spark make:migration LibreriaAddNome
```

```php
<?php
namespace App\Database\Migrations;
use CodeIgniter\Database\Migration;

class LibreriaAddNome extends Migration
{
    public function up()
    {
        $col = [
            'nome' => [
                'type' => 'VARCHAR',
                'constraint' => 255
                ]
            ];

        $this->forge->addColumn('libri', $col);
    }

    public function down()
    {
        $this->forge->dropTable('libri');
    }
    }
```
