
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
```

## custom methods

```php
$app->resource('post', ['like', 'trash', 'fork']);
```

will generate following addtional routing rules

```
$app->post('/post/:postId/like', 'post/like');
$app->post('/post/:postId/trash' 'post/trash');
$app->post('/post/:postId/fork', 'post/fork');
```

## subresources

declaring subresources

```php
$app->resource('post', 'comment', ['upvote', 'downvote']);
// /post/:postId/comment/:commentId
```

multilevel subresources

```php
$app->resource('post', 'comment', 'from', 'to');
// /post/:postId/comment/:commentId/from/:fromId/to/:toId
```

