

string will be send to client with content-type `text/html`

```php
$app->post('/test', function(){
	return "<pre>".var_export($this->body->asArray());
});
```

array will be encoded and send to client with content-type `application/json`

```php
$app->set('pretty');  // pretty print

$app->post('/test', function(){
	return $this->body;
});
```

int will be send as http status

```php
$app->post('/test', function(){
	return 201;
});
```
