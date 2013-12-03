
```php
return [
	'components' => [
		'db' => 'PDO', [
			'config' => [
				'dsn' => 'mysql:host=localhost;dbname=mysql',
				'username' => 'root',
				'password' => 'secret',
				'queries' => [
					'users' => 'select User,Host from user limit :offset,:limit',
				]
			]
		]
	]
];
```

```php
$app->get('/users', function($limit, $offset) {
	$user = $this->db->users->bind(['limit'=>$limit,'offset'=>$offset])->fetchAll();
	// or 
	$user = $this->db->users->bindInt('limit',$limit)->bindInt('offset',$offset)->fetchAll();
	return $user;
});
```

`noun->verb` style

```php
return [
	'components' => [
		'db' => 'PDO', [
			'config' => [
				'dsn' => 'mysql:host=localhost;dbname=mysql',
				'username' => 'root',
				'password' => 'secret',
				'queries' => [
					'users' => [
						'list' => 'select User,Host from user limit :offset,:limit',
					]
				]
			]
		]
	]
];
```

```php
$app->get('/users', function($limit, $offset) {
	$user = $this->db->users
		->bindInt('limit', $limit)
		->bindInt('offset', $offset)
		->list();
	// or 
	$user = $this->db->users->list(['limit'=>10, 'offset'=>0]);
	return $user;
});
```
