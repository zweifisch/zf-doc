

components are just classes attached to the $app instance,
`\zf\Mongo`, `\zf\Redis` and '\zf\Session' are available out of the box

```php
$app->register('mongo', '\zf\Mongo', $app->config->mongo);
$app->register('redis', '\zf\Redis');

// \zf\Mongo won't be initilazed unless $app->mongo is accessed
$app->mongo->users->findOne();
```

execute some additional code, when component is actually initialized

```php
$app->register('component', 'SomeClass', $arg1, $arg2)->initialized(function($component){
	$connected = $component->connect();
	$this->debug('component', $connected);
});
```
