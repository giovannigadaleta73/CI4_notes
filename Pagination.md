PAGINATION

Per usare la funzione di paginazione nel Controller usiamo i metodi già contenuti nel Model e li invio come argomento alla view. 

Nel Controller:

public function index() {

        $productsModel = model('Products');
    
        $data = [
            'products' => $productsModel->paginate(4),
            'pager' => $productsModel->pager
        ];
    
        return view('products/index',$data);
    }

La query può avere delle normali condizioni where:

[...]
'products' => $productsModel
->where('age >', 65)
->where('weight <', 70)
->paginate(4)

Nella view:

<?= $pager->links() ?>

Questo metodo richiama di template che posso personalizzare modificato la voce corrispondente in App\Config\Pager.php

public $templates = [
        'default_full'   => 'custom_full', //'CodeIgniter\Pager\Views\default_full',
        'default_simple' => 'CodeIgniter\Pager\Views\default_simple',
        'default_head'   => 'CodeIgniter\Pager\Views\default_head',
    ];

$pager->links  ===> 'default_full'
$pager->simpleLinks ===> 'default_simple'

Posso usare il template di default CodeIgniter\Pager\Views\default_full.php come base per crearne uno personalizzato (es. App\Views\custom_full.php) che verrà cercato nella cartella delle View.
Il template fornito da CI4 è preimpostato per Bootstrap, di conseguenza se si usa un altro framework CSS va modificato.
