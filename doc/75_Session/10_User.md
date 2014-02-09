
login example using the `user` component

```php
$app->middleware('is', function($role){
	if(!$this->user->is($role)){
		$this->redirect('/login');
	}
});

/**
 * @is Admin
 */
$app->get('/admin', function(){
	return $this->render('dashboard',['username'=>$this->user->username]);
});

$app->get('/login', function(){
	return $this->render('login');
});

$app->post('/login', function(){
	$user = $this->db->user->fetchOne([
		'username' => $this->body->login,
		'password' => $this->body->password,
	]);
	if($user){
		$this->user->login($user['id'], [
			'username' => $user['username'],
			'role' => $user['role'],
			'permissions' => $user['permissions'],
		]);
		return $this->redirect('/admin');
	}
	return $this->render('login');
});

$this->get('/logout', function(){
	$this->user->logout();
	$this->redirect('/login');
});
```
