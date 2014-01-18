
logging using Monolog

```sh
composer.phar require "monolog/monolog:*"
```

configuration in configs.php

```php
return [
	'components' => [
		'log' => [
			'channels' => [
				'default' => [
					'StreamHandler' => ['logs/log.log', 'DEBUG'],
					'FirePHPHandler',
				],
				'security' => [
					'StreamHandler' => ['logs/security.log', 'WARNING'],
				],
			],
		],
	],
];
```

use it inside a handler

```php
$this->log->addInfo("log from default logger");

$this->log->security->addWarning("log from security logger", [
	'key' => 'value'
]);
```
