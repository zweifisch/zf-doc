
helpers should be put in `helpers.php` or registered dynamically

if you have a lot them, put them in the `helpers` folder

register a helper

```php
$app->helper('doNothing', function($arg) {
	return $arg;
});
```

helper in `helpers.php`

```php
<?php

namespace helpers;

function loadUsers($ids) {
	return $this->db->find($ids);
}
```

invoke a helper

```php
$app->get('/', function() {
	$this->helper->doNothing(null);
	$this->helper->doSometing();
});
```
