
`configs.php` will be loaded if exists

`configs-$ENV.php` will be loaded if enviroment variable `ENV` is set

an array should be returned in configs.php

```php
$exports['key'] = 'value';

return $exports;
```

retrieve

```php
$app->get('key');
```


set

```php
$app->set('key','value');

$app->set('fancy');    // equivelant to $app->set('fancy', true);
$app->set('nofancy');  // equivelant to $app->set('fancy', false);

$app->set(['pretty', 'nofancy', 'key'=>'value']);
```

## predefined options

TBD
