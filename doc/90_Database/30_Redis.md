
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
			'default' => [
				'host'     => 'localhost',
				'pconnect' => true,
			],
		],
		// ...
	],
	// ...
];
```

```php
$app->get('/product/:id', function($id) {
	$this->redis->product->incr('view:'.$id);
});
```

```php
$app->get('/', function(){
	$this->redis->counter->incr(); // same as $this->redis->default->incr('cunter');
});
```

```php
$this->redis->foo->bar = 'val'; // same as $this->redis->hset('foo', 'bar', 'val');

$this->redis->foo->hget('bar'); // same as $this->redis->hget('foo', 'bar');
```
