
getting params from url

```php
/**
 * @param string $id id of product
 */
$app->get('products/:id', function($id) {
	$id === $this->params->id;  // true
});
```

optional params

```php
/**
 * @param string $id id of product
 */
$app->get('products/:id?', function($id=null) {
	// ...
});
```

## accessing params in query string

`/products?limit=20&offset=20&c=1`

```php
/**
 * @param mixed $c c for category
 * @param int $limit limit will be converted to int
 * @param int $offset
 */
$app->get('products', function($c, $limit=10, $offset=0) {
	// if $c is not set, 404 will be returned
});
```

## preprocessing of params

register a param handler

```php
$app->param('ids', function($value) {
	return explode(',', $value);
});
```

when params get accessed, the registered handler will be called

```php
/**
 * @param string $ids
 */
$app->get('products/:ids', function($ids) {
	// ids should be [1,2,3] if request path is 'products/1,2,3'
});

$app->get('users/:ids', function() {
	// handler won't get called if $this->params->ids is not accessed
});
```

usecase: preloading data

```php
$app->param('productId', function($id) {
	$this->product = function() use ($id) {
		return $this->db->findOne(['_id' => $id]);
	};
});

/**
 * @param string $productId id of product
 */
$app->get('product/:productId', function($productId) {
	return $this->product ? $this->product : 404;
});
```
