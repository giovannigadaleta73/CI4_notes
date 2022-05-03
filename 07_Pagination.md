# 7. PAGINAZIONE

Il Model mette a disposizione anche la paginazione. Posso attivare quella di default e poi modificarla per adattarla alle mie esigenze.

Dovrò agire sul Controller e sulla View

Nel Controller:

public function index() {

        $productsModel = model('Products');
    
        $data = [
            'products' => $productsModel->paginate(4),
            'pager' => $productsModel->pager
        ];
    
        return view('products/index',$data);
    }

nel file Controller sostituisco paginate() a findAll() e invio i dati alla view:

```php
        $LibriModel = model('Libri');
        $dati['libri'] = $LibriModel
            ->where('price <', 10)
            ->orderBy('id', 'ASC')
           // ->findAll(10)
            ->paginate(4);

        $dati['pager'] = $LibriModel->pager;
```

Nella view <mark>App\Views\Catalogo\index.php</mark> mi basta richiamare il comando:

```php
<?= $pager->links() ?>
```

In questo modo compariranno dei link per la paginazione.

Posso personalizzare la paginazione indicando nel file di configurazione <mark>App\Config\Pager.php</mark> di utilizzare un template alternativo:

```php
public $templates = [
 'default_full' => 'custom_full', //'CodeIgniter\Pager\Views\default_full',
 'default_simple' => 'CodeIgniter\Pager\Views\default_simple',
 'default_head' => 'CodeIgniter\Pager\Views\default_head',
 ];
```

il path del template sarà <mark>App\views\custom_full.php</mark> come base posso usare il template di default <mark>vendor\codeIgniter4\framework\system\Pager\Views\default_full.php</mark>.
Questo è preimpostato per Bootstrap, di conseguenza se si usa un altro framework CSS, il file andrà modificato.
