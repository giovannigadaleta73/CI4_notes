I comandi alla nostra applicazione vengono dati attraverso l'url. CI4 legge l'url inserito seguendo uno schema [ sito internet ] / [ comando ] / [ eventuale parametro ]

Nella versione più semplice il comando si compone di un nome del controller e di un suo metodo.  

Quindi basterà indicare nell'url una stringa come questa:

www.miosito.com/prodotti/edit/12

per richiamare il controller prodotti e usare il suo metodo modifica passando come parametro il numero 12.

Questo comportamento si può estendere rendendo modificando la corrispondenza tra il comando richiesto e l'indirizzo url digitato. Un motivo potrebbe essere quello di nascondere i nomi di classi e metodi così che  ad esempio potrei richiamare lo stesso comando scrivendo '*modifica*' anzichè '*products/edit*'

Queste modifiche si possono impostare inserendo delle routes nel file app\Config\Routes.php 

```php
$routes->get('/modifica/(:num)', 'Products::edit/$1')
```
