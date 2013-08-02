
make sure `phar.readonly` is set to `Off` in `php.ini`

enable `dist`, `$app->set('dist');`

```sh
php app.php dist app.phar
```

enable `extract`, `$app->set('extract');`

```sh
php app.phar extract /dest/path
```

