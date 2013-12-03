
lastModified

```php
$this->response->lastModified($timestamp);
```

cacheControl

```php
$this->response->cacheControl('public', 'must-revalidate', ['max-age'=> 60]);
```

redirect

```php
$this->response->redirect($url);
$this->response->redirect($url, true); // 301
```

jsonp

```php
$app->get('/products', 'jsonp:callback', function() {
	return iterator_to_array($this->mongo->products->find());
});
```

if `$_GET['callback']` is set, javascript will be returned, otherwise json will be returned
