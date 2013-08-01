
in configs.php
```php
$exports['mongo'] = [
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
];

return $exports;
```

```php
$app->register('mongo', '\zf\Mongo');

$app->on('error:*',function($data,$event){
	$this->mongo['logs.errors']->insert(['type'=>$event, 'data'=>$data]);
});

$app->get('/user/:id', function(){
	if($user = $this->mongo->users->findOne(['_id'=>$this->params->id])){
		$this->send($user);
	}else{
		$this->emit('error:user', ['id'=> $this->params->id])->send(404);
	}
});
```

