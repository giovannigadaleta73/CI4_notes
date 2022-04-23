# 

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

- [ ] Definizione del controller: avrà una pagina con un form per l'inserimento dei dati e questo form invierà i dati per la registrazione sullo stesso Controller con la route e il metodo save-user. Dopo una verifica che ad originare l'invio dei dati sia stato il form con metodo post viene eseguita un validazione e se riuscita allora avviene il salvataggio dei dati. Viente restituito un messaggio di Successo o Fallimento. I dati dal form vengono presi con il metogo getVar("campo"). (nel corso viene usato jQuery per l'invio dei dati al db)
  
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
