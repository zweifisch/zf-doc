
getting params from url

```php
$app->get('products/:id', function($id) {
	$id == $this->params->id;  // true
});
```

optional params

```php
$app->get('products/:id?', function() {
	if($this->params->id){
		// show product by id
	} else {
		// $this->params->id is null, list all products
	}
});
```

## accessing params in query string

`/products?limit=20&offset=20&c=1`

```php
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
$app->get('products/:ids', function($ids) {
	// ids should be [1,2,3] if request path is 'products/1,2,3'
});

$app->get('users/:ids', function() {
	// handler won't get called if $this->params->ids is not accessed
});
```

usecase: preloading data

```php
$app->param('product_id', function($id) {
	$this->product = function() use ($id) {
		return $this->db->findOne(['_id' => $id]);
	};
});

$app->get('product/:product_id', function($product_id) {
	return $this->product ? $this->product : 404;
});
```

`$product_id` must be put in the handler's arguments list or be accessed using `$this->params->product_id` otherwise the param handler above won't be called; also note that `$this->product` won't be evaluated until it's accessed
