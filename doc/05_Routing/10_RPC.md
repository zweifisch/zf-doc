
[jsonrpc 2.0 specification](http://www.jsonrpc.org/specification)

```php
$app->rpc('/gateway', 'handlers');
```

request body

```javascript
{
	"jsonrpc": "2.0",
	"method": "job.start",
	"params": ["param", "param2"],
	"id": 512
}
```

will be routed to `handlers/job/start.php`

```php
<?php
return function($param, $param2) {
	return "job started";
};
```

defining user error codes

```php
$app->set('jsonrpc codes', [
	-32001 => 'Database write failed',
	-32002 => 'Upstream api time out',
]);
```

return an error

```php
return function() {
	return $this->error(-32001, $extraInfo);
};
```
