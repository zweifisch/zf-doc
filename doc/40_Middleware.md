
middleware is a way to map a request to multiple functions, samller and more reusable functions

## a middleware for permission controll

```php
$app->middleware('can', function($args) {
	if(!$this->user->can($args)){
		return 403;
	}
});

$app->delete('/post/:id', 'can:DeletePost', function() {
	return $this->db->delete(['_id'=> $id])
});
```

same thing without middleware

```php
$app->delete('/post/:id', function($id) {
	// check manually in each handler
	if($this->user->canDeletePost) {
		return $this->db->delete(['_id'=> $id]);
	}
	return 403;
});
```

### middleware as decorators

```php
/**
 * @can DeletePost
 */
return function($id){
	return $this->db->delete(['_id'=> $id]);
}
```

### writing a middleware

a middlware for http basic auth

```php
$app->middleware('auth', function($user, $passwd) {
	if($this->get('PHP_AUTH_USER') != $user
		|| $this->get('PHP_AUTH_PW') != $passwd) {
		$this->header('WWW-Authenticate', ['Basic realm'=> 'Login Required']);
		$this->status(401);
		return 'Unauthorized';
	}
});
```

If `null` or a closure is returned from the middleware, the next middleware will be called, otherwise the returned result will be interpreted as the response and the rest middlewares will be skipped.

The closures returned from the middlewares will be called one by one in reversed order once the response is available, and the response will be passed as an argument to those closures, so that the response can be modified.

standalone middlewares should be located in `middlewares` by default

