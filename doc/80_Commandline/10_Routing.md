
passing arguments

```php
$app->cmd('mv <src> <target>', function(){
	$src = $this->params->src;
	$target = $this->params->target;
});
```

options

```php
$app->set('pretty');

$app->cmd('mv <src> <target>', function(){
	return $this->params;
})->options(['overwrite','interactive']);
```

```bash
php cli.php mv --overwrite foo bar
```

```javascript
{
	"overwrite": true,
	"interactive": false,
	"src": "foo",
	"target": "bar"
}
```

options with values

```php
$app->set('pretty');

$app->cmd('mail <to>', function(){
	return $this->params;
})->options(['cc'=>'','subject'=>'untitled']);
```

```bash
php cli.php mail --cc=foo@mail.com bar@mail.com
```

```javascript
{
	"cc": "foo@mail.com",
	"subject": "untitled",
	"to": "bar@mail.com"
}
```
