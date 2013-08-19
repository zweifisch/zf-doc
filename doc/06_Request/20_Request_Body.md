
request body should be encoded as `application/json` or `application/x-www-form-urlencoded`

get an optional field

```js
{
	"name": "foo",
	"age": 0
}
```

```php
$app->post('user',function(){
	$name = $this->body->name->asStr(); // name is required
	$age = $this->body->age->asInt(20); // age is optinal, default is 20
});
```

## validation

`null` will returned if the key is not set, or failed to pass the validation rules

```php
$app->post('user',function(){
	$age = $this->body->age->between(1,200)->asInt() or die();
});
```

alternativly you can listen for the `VALIDATION_FAILED` event

```php
$app->post('user',function(){
	$age = $this->body->age->between(1,200)->asInt();
});

$app->on(zf\VALIDATION_FAILED, function($detail){
	$this->send(400, $detail);
});
```

using multiple keys

```php
$app->post('user',function(){
	$user = $this->body->extract([
		'age:Int' => 'default:20|between:1,200',
		'name' => 'minlen:4|maxlen:20',
		'password' => 'minlen:8|maxlen:100',
	]) or die();
	$this->mongo->users->insert($user);
});
```

## file upload

```php
$app->post('user',function(){
	$file = $this->body->avatar->asFile();
	$this->mongo->avatars->insert([
		'avatar'=> new MongoBinData($file->content),
		'extension'=> $file->extension
	]);
});
```

