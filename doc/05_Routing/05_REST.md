
declaring a rousource

```php
$app->resource('post');
```

which is equivelent to

```php
$app->get('/post', 'post/index');
$app->get('/post/new', 'post/new');
$app->post('/post', 'post/create');
$app->get('/post/:postId', 'post/show');
$app->get('/post/:postId/edit', 'post/edit');
$app->put('/post/:postId', 'post/update');
$app->patch('/post/:postId', 'post/modify');
$app->delete('/post/:postId', 'post/destroy');
// and for custom methods
$app->post('/post/:postId/:action', 'post/:action');
```

## subresources

declaring subresources

```php
$app->resource('post/comment');
// /post/:postId/comment/:commentId
```

## path prefix

```php
$app->resource('v2', 'post');
```

## multiple resources

```php
$app->resource('v2', ['post', 'user']);
$app->resource(['post', 'user', 'user/avatar']);
```
