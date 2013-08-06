
`zf\App` extends `Laziness`

assign a closure to a Laziness instance and access it later will get the closure evaluated, and the result will be cached

```php
$app->products = function(){
	$this->mongo->products->find();
};

$app->get('products', function(){
	return iterator_to_array($this->products);  // db query won't be send until this line
});
```

combined with param handlers

```php
$app->param('products', function($value){
	$this->product = $this->helper->delayed->loadProduct($value);
	return $value;
});

$app->get('products/:products', function(){
	return $this->products;
});
```

