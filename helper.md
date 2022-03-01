### view

Certamente l'helper più usato è `view('file-view', $array_dati) `per elaborare e mostrare (fare il render di) una view. 

Posso usarlo in una route:

```php
$routes->get("home", function () {
    return view("wellcome_page", $array_dati);
});
```

oppure all'interno di un controller:

```php
class ElencoDipendenti extends BaseController
{
    public function home()
    {
        $array_dati = ["name" => "Charlie", "age" => 30];
        return view("wellcome_page", $array_dati);
    }
}
```

form_open

form_input

form_password

form_textarea

form_submit

form_button

form_close

App\Config\Database.php

App\Database\Migrations\

App\Database\Seeds\
