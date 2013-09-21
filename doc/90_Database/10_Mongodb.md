
install mongo extension `sudo pecl install mongo`

configuration in configs.php

```php
return [
	'components' => [
		'mongo:\zf\Mongo' => [
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
		],
	],
];

```

query

```php
$app->get('/user/:id', function(){
	if($user = $this->mongo->users->findOne(['_id'=>$this->params->id])){
		$this->send($user);
	}else{
		$this->emit('error:user', ['id'=> $this->params->id])->send(404);
	}
});
```

accessing a collection with a dot in name

```php
$app->on('error:*',function($data, $event){
	$this->mongo['logs.errors']->insert(['type'=>$event, 'data'=>$data]);
});
```

GridFS

```php
return [
	'components' => [
		'mongo:zf\Mongo' => [
			'posts','attchments:GridFS' => [
				'url'        => 'mongodb://localhost:27017',
				'database'   => 'project',
			],
		],
	],
];
```

```php
$app->post('/attachment', function(){
	$this->mongo->attchments->storeUpload('attachment');
});
```
