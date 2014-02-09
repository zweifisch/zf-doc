
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
$app->post('/user', 'user/create');  // load from handlers/user.php
```

inside `handlers/user.php`

```php
<?php

namespace user;

function create() {
	// the unparsed request body can be accessed as $this->request->body
	// 'mongo' is a component, which will be covered later
	$this->mongo->users->insert($this->body);
	return ['ok'=>true, 'msg'=>'user created'];
}
```
