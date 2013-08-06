
register as a component

```php
$app->register('session', '\zf\Session');
```

a login example

```php
$app->get('/admin', function(){
	if($this->session->login){
		return $this->render('dashboard',['login'=>$this->session->login]);
	}
	$this->redirect('/login');
});

$app->get('/login', function(){
	return $this->render('login');
});

$app->post('/login', function(){
	$user = $this->db->user->fetchOne([
		'login' => $this->body->login->asStr(),
		'password' => $this->body->password->asPassword(),
	]);
	if($user){
		$this->session->set([
			'login' => $user['login'],
			'id' => $user['id'],
		]);
		return $this->redirect('/admin');
	}
	return $this->render('login');
});

$this->get('/logout', function(){
	$this->session->destroy();
	$this->redirect('/login');
});
```
