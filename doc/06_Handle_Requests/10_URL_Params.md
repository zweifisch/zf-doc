
```php
$app->get('products/:id', function(){
	$id = $this->params->id;
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

accessing params in query string

`/products?limit=20&offset=20&c=1`

```php
$app->get('products', function(){
	$limit = $this->query->limit->asInt(10);
	$offset = $this->query->offset->asInt(0);
	$category = $this->query->c->asStr('');
	$keyword = $this->query->q->asStr('');
	if($search){
		// query db with keyword
	}else{
		// list all products
	}
});
```

preprocessing of params

```php
$app->get('products/:ids', function(){
	$this->params->ids;
});

$app->get('users/:ids', function(){
	$this->params->ids;
});

$app->param('ids', function($value){
	return explode(',', $value);
});
```
