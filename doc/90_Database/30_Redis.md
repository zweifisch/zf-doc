
install the redis extension [phpredis](https://github.com/nicolasff/phpredis)

configuration

```php
$exports['redis'] = [
	'product' => [
		'host'     => 'localhost',
		'pconnect' => true,
	]
];

return $exports;
```

register as a component

```php
$app->register('redis','\zf\Redis');
```

```
$app->get('/product/:id', function(){
	$this->redis->product->incr('view:'.$this->params->id);
});
```

## use predefined keys

TBD
