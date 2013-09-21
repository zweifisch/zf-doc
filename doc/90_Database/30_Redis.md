
install the redis extension [phpredis](https://github.com/nicolasff/phpredis)

configuration in configs.php

```php
return [
	'components' => [
		'redis' => [
			'product' => [
				'host'     => 'localhost',
				'pconnect' => true,
			],
		],
		// ...
	],
	// ...
];
```

```
$app->get('/product/:id', function(){
	$this->redis->product->incr('view:'.$this->params->id);
});
```

## use predefined keys

TBD
