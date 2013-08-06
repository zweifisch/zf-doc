
closure as handler

```php
$app = new zf\App;
$app->get('/ip', function(){
	return $this->clientIP();  // $app can be accessed using $this
});
$app->run();
```

using external handler

```php
$app->post('/users', 'users/create');  // load from handlers/users/create.php, path is configurable
```

handlers/user/create.php

```php
<?php

return function(){
	$this->mongo->users->insert($this->request->body->asArray());
	$this->status(201);
	return ['ok'=>true, 'msg'=> 'user created'];
};
```
