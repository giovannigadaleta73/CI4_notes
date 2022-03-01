## - - MIGRATION

Le migration sono file che contengono istruzioni per creare e modificare le tabelle del nostro progetto. Sostituiscono e rendono rapide tutte quelle operazioni fatte manualmente con i vari programmi di gestione dei database come phpMyAdmin. Il nome della migration segue la notazione PascalCase.

CLI> php spark make:migration CreateAnimals

Dopo averla creata si avvia con

CLI> php spark migrate

Con questo comando viene generato una semplice struttura con due metodi: up e down [1], per la creazione o modifica delle tabelle e il ripristino alla situazione iniziale [2].

[1][...]

class CreateAnimals extends Migration

{

    public function up()

    {

        //

    }

    public function down()

    {

        //

    }

}

In sequenza il metodo up conterrà:

si creano i campi ($this->forge->addField([ … ]);)

si indica l’indice ($this->forge->addField('id');)

e infine il nome della tabella ($this->forge->createTable('animals');)

Mentre nel metodo down ($this->forge->dropTable('products');)

per le specifiche: [vendor\codeigniter4\framework\system\Database\Forge.php]

[2][...]

public function up()

{

        $this->forge->addField([

            'id' =>  [

                'type' => 'INT',

                'constraint' => 11,

                'unsigned' => true,

                'auto_increment' => true,

            ],

            'title' => [

                'type' => 'VARCHAR',

                'constraint' => 255,

                'unique' => true,

            ],

            'description' => [

                'type' => 'TEXT',

                'null' => true,

            ],

            'price' => [

                'type' => 'DECIMAL',

                'constraint' => '10,2',

            ]

        ]);

        $this->forge->addKey('id');

        $this->forge->createTable('animals');

}

public function down()

{

        $this->forge->dropTable('animals');

}
