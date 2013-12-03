
closure as handler

```php
$app = new zf\App;
$app->get('/ip', function(){
	return $this->request->ip;  // $app can be accessed using $this
});
$app->run();
```

using external handler

```php
$app->post('/users', 'users/create');  // load from handlers/users/create.php
```

inside `handlers/user/create.php`

```php
<?php

return function(){
	// the unparsed request body can be accessed as $this->request->body
	$this->mongo->users->insert($this->body);
	$this->response->status = 201;
	return ['ok'=>true, 'msg'=> 'user created'];
};
```
