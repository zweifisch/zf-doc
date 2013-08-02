
## install

install using [composer](http://getcomposer.org/)
```sh
composer.phar require 'zweifisch/zf:*'
```

if you're not using composer, download soruce code [here](https://github.com/zweifisch/zf/tags)

```php
require 'vendor/autoload.php'; #  require 'zf/zf.php'; if you are not using composer

$app = new zf\App();

$app->get('/hello/:name', function(){
	$this->send(['hello' => $this->params->name]);
})->run();
```
