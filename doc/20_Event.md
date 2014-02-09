
registering and triggering events

```php
$app->on('user:hit', function($data) {
	$this->mongo['events.user']->insert(['user'=>$data['_id']);
});

$app->on('user:hit', function($data) {
	$this->redis->users->zincrby('hotusers', 1, $data['_id']);
});

$app->get('/user/:id', function($id) {
	$user = $this->mongo->user->findOne(['_id'=>$id]);
	$this->emit('user:hit', $user);
	return $user;
});
```

handler with highest priority get called first, the default priority is `0`

```php
$app->on('event', function(){
	// will be called after all handlers
})->priority(-1);
```

listening for multiple events

```php
$app->on('user:*', function($data, $event){
	// will get called for `user:login`, `user:logout` etc.
});
```

registering event handlers using the `$app->onSomeEvent` method

```php
$app->onEvent($callback); // same as $app->on('event', $callback);
```

to stop an event, return a truthy value in the handler

### predefined events

'exception', 'error', 'shutdown'

```php
$app->onShutdown(function() {
	echo 'bye';
});
```

