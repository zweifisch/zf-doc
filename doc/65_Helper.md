
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
	$this->helper->donothing(null);
	$this->helper->otherhelper(); // load from helpers folder
});
```

register helper from `helpers` folder

```php
$app->helper(['myhelper', 'otherhelper']);
```

registrated helpers can be accessed as `$this->myhelper();`

## delayed

$app->helper is an instance of 'ClosureSet', which has a property `deplayed`

```php
$this->helper->delayed->loadProduct($id);
```

is equivelent to 

```php
function(){
	$this->helper->loadProduct($id);
}
```
