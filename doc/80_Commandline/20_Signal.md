
sigint example

```php
declare(ticks = 1);
$app->cmd('forever', function(){
	$this->log('presss ctrl-c to quit');
	$this->done = false;
	$this->counter = 0;
	while(!$this->done){
		$this->log('%s secs elapsed', ++$this->counter);
		sleep(1);
	}
	$this->log('done');
});

$app->sigint(function(){
	$this->log('stopping');
	$this->done = true;
});
```

other signals

```php
$app->sigusr1(function(){
	$this->log('USR1 caught');
});
```
