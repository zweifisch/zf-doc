
use the original PDO
```php
$app->register('db', '\PDO', $dsn, $user, $password);
```

use the wrapped PDO
```php
// configs.php
$exports['db'] = [
	'dsn' => 'mysql:host=localhost;dbname=mysql',
	'username' => 'root',
	'password' => 'secret',
	'queries' => [
		'users' => 'select User,Host from user limit :offset,:limit',
	]
];
return $exports;
```

```php
$app->register('db','\PDO');

$app->get('/users', function(){
	$user = $this->db->users->bind(['limit'=>10,'offset'=>0])->fetchAll();
	// or 
	$user = $this->db->users->bindInt('limit',10)->bindInt('offset',0)->fetchAll();
	$this->send($user);
});
```

```php
// configs.php
$exports['db'] = [
	'dsn' => 'mysql:host=localhost;dbname=mysql',
	'username' => 'root',
	'password' => 'secret',
	'queries' => [
		'users' => [
			'list' => 'select User,Host from user limit :offset,:limit',
		]
	]
];
return $exports;
```

```php
$app->register('db','\PDO');

$app->get('/users', function(){
	$user = $this->db->users
		->bindInt('limit',10)
		->bindInt('offset',0)
		->list();
	// or 
	$user = $this->db->users->list(['limit'=>10, 'offset'=>0]);
	$this->send($user);
});
```
