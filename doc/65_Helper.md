
helpers should be put in the `helpers` folder, or registered dynamically

register a helper

```php
$app->helper('donothing', function($arg){
	return $arg;
});
```

invoke a helper

```php
$app->get('/', function(){
	$this->helper->donothing(null); // $this->donothing(null); is also valid
	$this->helper->otherhelper(); // load from helpers folder
});
```

register helper from `helpers` folder

```php
$app->helper(['myhelper', 'otherhelper']);
```

registrated helpers can be accessed as `$this->myhelper();`
