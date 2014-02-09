
passing arguments

```php
$app->cmd('mv <src> <target>', function($src, $target) {
	// ...
});
```

options

```php
$app->set('pretty');

/**
 * @param string $src
 * @param string $target
 * @param bool $overwrite
 */
$app->cmd('mv <src> <target>', function($src, $target, $overwrite=false) {
	return $this->params;
});
```

```bash
php cli.php mv --overwrite foo bar
```

```javascript
{
	"overwrite": true,
	"src": "foo",
	"target": "bar"
}
```
