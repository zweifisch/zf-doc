
a login example

```php
$app->get('/admin', function() {
	if($this->session->login) {
		return $this->render('dashboard',['login'=>$this->session->login]);
	}
	$this->redirect('/login');
});

$app->get('/login', function() {
	return $this->render('login');
});

$app->post('/login', function() {
	$user = $this->db->user->fetchOne([
		'login' => $this->body->login,
		'password' => $this->body->password,
	]);
	if($user) {
		$this->session->mset([
			'login' => $user['login'],
			'id' => $user['id'],
		]);
		return $this->redirect('/admin');
	}
	return $this->render('login');
});

$this->get('/logout', function() {
	$this->session->destroy();
	$this->redirect('/login');
});
```
