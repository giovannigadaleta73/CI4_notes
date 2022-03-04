## Chapter 1: CodeIgniter 4 Basics

#### Complete CodeIgniter 4 Basics Tutorial

+ [x] caratteristiche e origine di CI4

+ [x] installazione: manuale, github, composer
  
  ```shell
  composer create-project codeigniter4/appstarter codeigniter-4
  ```

+ [x] struttura cartelle

+ [x] setup di .env

+ [x] panoramica su Controller, route e view che troviamo di default

+ [x] comandi per creare un Controller, una route 

#### CodeIgniter 4 Views And Layouts Tutorial

- [x] Render a View File in CodeIgniter 4

- [x] Passing Data to View File
  
  ```php
  return view("my-file", $data);
  ```

- [x] Create a Master Layout in CodeIgniter 4 
  
  ```php
  <?= $this->renderSection("content"); ?>
  ```
  
  ```php
  <?=$this->extend("layout/master")?>
  
  <?=$this->section("content")?>
      
  <?=$this->endSection()?>
  ```

- [x] Including Styles and Scripts to CodeIgniter 4 Layout
  
  ```php
  <link rel="stylsheet" href="<?= base_url('public/css/style.css') ?>"/>
    
  <?= link_tag('public/css/style.css') ?>
  ```

- [x] Including Partial Files Or Sub views
  
  ```php
  $this->include(“partials/header”)
  ```



## Chapter 2: CodeIgniter 4 with MySQL

Creo un db e faccio le prime operazioni di inserimento dati

- [ ] Add Routes
  
  ```php
  $routes->get("add-user", "UserController::addUser");
  $routes->post("save-user", "UserController::saveUser");
  ```

- [ ] Creazione del Model e configurazione della tabella indicando tra le atre cose i campi modificabili dai nostri script.
  
  ```shell
  php spark make:model User --suffix
  ```

- [ ] Creazione del Controller
  
  ```shell
  php spark make:controller User --suffix
  ```

- [ ] Definizione del controller: avrà una pagina con un form per l'inserimento dei dati e questo form invierà i dati per la registrazione sullo stesso Controller con la route e il metodo save-user. Dopo una verifica che ad originare l'invio dei dati sia stato il form con metodo post viene eseguita un validazione e se riuscita allora avviene il salvataggio dei dati.Viente restituito un messaggio di Successo o Fallimento. I dati dal form vengono presi con il metogo getVar("campo"). (nel corso viene usato jQuery per l'invio dei dati al db)
  
  ```php
  ...
  if ($this->request->getMethod() == "post")
  ...
  if (!$this->validate($rules))
  ...
  "name" => $this->request->getVar("name")
  ...
  return $this->response->setJSON($response);
  ```

- [ ] 

- [ ] 

## Chapter 3: CodeIgniter 4 Validation

## Chapter 4: CodeIgniter 4 Security

## Chapter 5: CodeIgniter 4 Helpers & Services

## Chapter 6: CodeIgniter 4 Advance

## Chapter 7: CodeIgniter 4 REST APIs


