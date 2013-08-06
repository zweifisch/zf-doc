
lastModified

```php
$this->lastModified($timestamp);
```

cacheControl

```php
$this->cacheControl('public', 'must-revalidate', ['max-age'=> 60]);
```

jsonp

```php

$app->get('/products', function(){
	$this->set('jsonp', 'callback');
	return iterator_to_array($this->mongo->products->find());
});
```

if `$_GET['callback']` is set, javascript will be returned, otherwise json will be returned
