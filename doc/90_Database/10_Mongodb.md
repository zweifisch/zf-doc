
install mongo extension `sudo pecl install mongo`

configuration in configs.php

```php
'components' => [
	'mongo' => 'Mongo', [
		'collections' => [
			'users','articles' => [
				'url' => 'mongodb://10.0.1.1:27017,10.0.1.2:27017',
				'database'=> 'production',
				'options' => [
					'replicaSet'=> 'rs0',
					'readPreference' => \MongoClient::RP_SECONDARY_PREFERRED,
				],
			],
			'logs.errors' => [
				'url' => 'mongodb://10.0.2.1:27017',
				'database'=> 'production',
			],
		]
	],
],
```

query

```php
/**
 * @param string $id
 */
$app->get('/user/:id', function($id) {
	if($user = $this->mongo->users->findOne($id)) {
		return $user;
	} else {
		return 404;
	}
});
```

accessing a collection with a dot in name

```php
$this->mongo['logs.errors']->insert($data);
```

GridFS

```php
'components' => [
	'attachments' => 'MongoGridFS', [
			'url'        => 'mongodb://localhost:27017',
			'database'   => 'project',
		]
	],
],
```

```php
$app->post('/attachment', function() {
	$this->gfs->storeUpload('attachment');
});
```
