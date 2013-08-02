
restful routing

## Resource

declare a rousource

```php
$app = new zf\App;
$app->resource('posts');
$app->run();
```

which is equivelent to

```php
$app->get('/posts', 'posts/index'); // handlers/posts/index.php
$app->post('/posts', 'posts/create');
$app->get('/posts/:posts', 'posts/show');

$app->put('/posts/:posts', 'posts/update');
$app->patch('/posts/:posts', 'posts/modify');
$app->delete('/posts/:posts', 'posts/destroy');

$app->post('/posts/:posts/:action', 'posts/$action'); // handlers/posts/$action.php

$app->get('/posts', 'posts/new');
$app->get('/posts/:posts/edit', 'posts/edit');
```

