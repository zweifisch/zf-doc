
declare a rousource

```php
$app->resource('posts');
```

it is equivelent to

```php
$app->get('/posts', 'posts/index');
$app->post('/posts', 'posts/create');
$app->get('/posts/:posts', 'posts/show');

$app->put('/posts/:posts', 'posts/update');
$app->patch('/posts/:posts', 'posts/modify');
$app->delete('/posts/:posts', 'posts/destroy');

$app->post('/posts/:posts/:action', 'posts/$action');

$app->get('/posts/:posts/edit', 'posts/edit');
```
