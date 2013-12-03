
`configs.php` will be loaded if exists

`configs-$ZF_ENV.php` will be loaded if enviroment variable `ZF_ENV` is set

an array should be returned in config file

```php
return [
	'key' => 'value';
];
```

retrieve

```php
$app->get('key'); // if key is not set, `null` will be returned

$app->get('KEY'); // if the key starts with a upper case letter, $_SERVER['KEY'] will be returned
```

set

```php
$app->set('key','value');

$app->set('pretty');    // equivelant to $app->set('pretty', true);
$app->set('nopretty');  // equivelant to $app->set('pretty', false);

$app->set(['pretty', 'mockup', 'key'=>'value']);
```
