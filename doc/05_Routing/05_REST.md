
declaring a rousource

```php
$app->resource('posts');
```

which is equivelent to

```php
$app->get('/posts', 'posts/index');
$app->get('/posts/new', 'posts/new');
$app->post('/posts', 'posts/create');
$app->get('/posts/:posts', 'posts/show');
$app->get('/posts/:posts/edit', 'posts/edit');
$app->put('/posts/:posts', 'posts/update');
$app->patch('/posts/:posts', 'posts/modify');
$app->delete('/posts/:posts', 'posts/destroy');
```

## custom methods

```php
$app->resource('posts', ['like', 'trash', 'fork']);
```

will generate following addtional routing rules

```
$app->post('/posts/:posts/like', 'posts/like');
$app->post('/posts/:posts/trash' 'posts/trash');
$app->post('/posts/:posts/fork', 'posts/fork');
```

## subresources

declaring subresources

```php
$app->resource('posts', 'comments', ['upvote', 'downvote']);
// /posts/:posts/comments/:comments
```

multilevel subresources

```php
$app->resource('posts', 'comments', 'from', 'to');
// /posts/:posts/comments/:comments/from/:from/to/:to
```

