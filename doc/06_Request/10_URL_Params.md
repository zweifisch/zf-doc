
get params from url

```php
$app->get('products/:id', function($id){
	$id == $this->params->id;  // true
});
```

optional params

```php
$app->get('products/:id?', function(){
	if($this->params->id){
		// show product by id
	}else{
		// $this->params->id is null, list all products
	}
});
```

## accessing params in query string

`/products?limit=20&offset=20&c=1`

```php
$app->get('products', function(){
	$limit = $this->query->limit->asInt(10);
	$offset = $this->query->offset->asInt(0);
	$category = $this->query->c->asStr('');
});
```

or more concisely

```php
$app->get('products', function($c, $limit=10, $offset=0) {
	// if $c is not set, 404 will be returned
});
```

## preprocessing of params

register a param handler

```php
$app->param('ids', function($value){
	return explode(',', $value);
});
```

when params get accessed, the registered handler will be called

```php
$app->get('products/:ids', function(){
	$this->params->ids;  // '1,2,3' will be turned into [1,2,3]
});

$app->get('users/:ids', function(){
	// handler won't get called if $this->params->ids is not accessed
});
```

eager handlers always get called

```php
$app->param('productIds', function($value){
	$ids = explode(',', $value);
	// `delayed` will return a closure, see Helper
	$this->products = $this->helper->delayed->loadProducts($ids);
	return $ids;
})->eager();
```

```php
$app->get('products/:productIds', function(){
	return $this->products;
});
```
