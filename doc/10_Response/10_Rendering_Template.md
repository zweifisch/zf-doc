
loading templates

```php
$app->get('/dashboard', function(){
	return $this->render('dasboard');  // views/dashboard.php
});
```

passing variables

```php
$app->get('/dashboard', function(){
	return $this->render('dasboard', ['date'=> date('Y-m-d')]);
});
```

dashboard.php

```html
<html>
<span> today is <?= date?> </span>
<span> <?= $this->helper->fortune()?> </span>
</html>
```

## using mustache

configuration in configs.php

```
return [
	'components' => [
		'engine' => 'Mustache', [
			'path' => 'views',
			'extension' => '.mustache',
		],
	],
];
```

```php
$app->get('/', function(){
	// render index.mustache
	return $this->render('index', [
		'foo' => 'bar',
		'upper' => $this->helper->upper,
	]);
});
```
