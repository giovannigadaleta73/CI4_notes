## IF

```php
<?php if(isset($validation)): ?>

 // Codice eseguito se if è true

 <?php endif; ?>
```

# 

## LINK

```php
<a class="navbar-item" href="<?= site_url(['login', 'logout']) ?>">Logout</a>

<a class="navbar-item" href="<?= site_url(['products']) ?>">Elenco</a>

<a class="navbar-item" href="<?= site_url(['products', 'add']) ?>">Nuovo</a>
```

## 

## FORM INVIO

```php
<?= form_open(current_url(), ['method' => 'post']) ?>

<?= form_label('Title', 'title', ['for' => 'Title', 'class' => 'form-label']) ?>

<?= form_input('title', '', ['class' => 'form-control']) ?>

<?= form_textarea('description', '', ['class' => 'form-control']) ?>

<?= form_input('price', '', ['class' => 'form-control', 'min' => 0, 'step' => '.1'], 'number') ?>

<?= form_submit('submit', 'Submit', ['class' => 'btn btn-primary']) ?>

<?= form_close() ?>
```

## 

## FORM RICEZIONE

Ricevo i dati di un form (pagina che richiama se stessa tramite un Controller Products.php e una funzione add() ) attivo l’helper(‘form’) e avrò così a disposizione alcuni metodi che elaborano i dati del form:

```php
$this->request->getMethod() // lo uso per verificare il method del form

$this->validate([

'title' =>'required|min_length[10]',

'description' =>'required|min_length[50]',

'price' =>'required|decimal']); // istruzioni per la validazione

$this->validator // elenca gli errori trovati durante la validazione

$this->request->getPost() // restituisce i dati del form
```

## helper()

Posso chiamare l’helper nella funzione add() del mio controller

```php
app\Controllers\Products.php

    public function add() {
        helper(‘form’);
        …
}
```

gli errori li trovo in 

$validation = $this->validator e li visualizzo con 

<?= $validation->listErrors() ?>

oppure posso attivarlo per tutti i controller da 

app/Controllers/BaseController.php

    protected $helpers = [‘form’];

## BOOTSTRAP FORM

form-group

    form-label

    form-control (per input e textarea)

## PHP

<mark>compact()</mark>

```php
$firstname = "Peter";
$lastname = "Griffin";
$age = "41";

$name = array("firstname", "lastname");
$result = compact($name, "location", "age");

print_r($result); 
// Array ( [firstname] => Peter [lastname] => Griffin [age] => 41 )
```
