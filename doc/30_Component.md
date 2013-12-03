register components in configs.php

```php
return [
	'components' => [
		'mongo' => 'Mongo', [
			'collections' => [
				'users','posts' => [
					'url'        => 'mongodb://localhost:27017',
					'database'   => 'project',
			],
		],
		'redis' => 'Redis', [
			'dbs' => [
				'default' => [
					'host'     => 'localhost',
					'pconnect' => true,
				],
			],
		],
	],
];
```

accessing components

```
$app->mongo->users->findOne();
```

## register componets on the fly

```php
$app->register('db', '\ns\SomeDB', ['host' => $host, 'port' => $port]);
```

or using a closure

```php
$app->register('myComponent', function(){
	return new \ns\SomeComponent();
});
```

execute some additional code when the component is actually initialized

```php
$app->register('db', '\ns\SomeDB', ['url' => $url])->initialized(function($db) {
	$connected = $db->connect();
});
```

## component depends on other components

```php
return [
	'components' => [
		'httpclient' => '\HTTPClient',
		'restclient' => '\RestClient' => [
			'baseurl' => 'http://restserver.io'
		],
	],
];
```

```php
class RestClient
{
	function __construct($baseurl, $httpclient)
	{
		// $httpclient is an instance of \HTTPClient;
	}
}
```
