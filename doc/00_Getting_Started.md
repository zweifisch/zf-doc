
install using [composer](http://getcomposer.org/)
```sh
composer.phar require 'zweifisch/zf:*'
```

if you're not using composer, download soruce code [here](https://github.com/zweifisch/zf/tags)

create a index.php

```php
<?php

require 'vendor/autoload.php'; #  require 'zf/zf.php'; if you are not using composer

$app = new zf\App();

$app->get('/hello/:name', function(){
	return ['hello' => $this->params->name];
})->run();
```

start the built-in php server

```bash
php -S 0.0.0.0:5000
```
