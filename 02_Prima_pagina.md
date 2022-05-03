# 2. PRIMA PAGINA

## Creare una pagina nuova

Creaiamo una semplice pagina statica

+ il Controller
  
  creare il comando per aprire una nuova pagina: 

```shell
php spark make:controller Catalogo
```

viene creato: <mark>App\Controllers\Catalogo.php</mark>

All'interno di Catalogo.php

```php
public function index()
    {
        $dati['libri'] = ['Il Signore degli Anelli', 'Il giovane Holden', '1984'];
        return view('catalogo/index', $dati);
    }    
```

creo una pagina che verrà richiamata dal Controller in

<mark>App\Views\catalogo\index.php</mark>

```php
<section class="columns is-multiline">
<ul>

<?php foreach ($libri as $titolo) : ?>
    <li>
    TITOLO: <?= $titolo ?>
    </li>
<?php endforeach; ?>

</ul>
</section>
```

questa pagina è raggiungibile con gli url

+ nome.sito/controller ==> http://localhost:8080/catalogo

+ nome.sito/controller/index  ==> http://localhost:8080/catalogo/index
