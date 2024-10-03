### index.php
```php
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Login</title>
</head>
<body>
	<?php session_start(); ?>

	<h1>Login</h1>

	<form action="handleForm.php" method="POST">
		<p>Username: <input type="text" placeholder="" name="firstName"></p>
		<p>Password: <input type="password" placeholder="" name="password"></p>
		<p><input type="submit" value="Submit" name="submitBtn"></p>
	</form>

	<form action="unset.php" method="POST">
		<p><input type="submit" value="Logout" name="logoutBtn"></p>
	</form>

	<h2>
		<?php
		if(isset($_GET['error']) && $_GET['error'] == 'already_logged_in') {
			$loggedInUser = htmlspecialchars($_GET['user']);
			echo "$loggedInUser is already logged in. Wait for the user to log out first.";
		}
		elseif(isset($_SESSION['firstName']) && isset($_SESSION['password'])) {
			echo "User logged in: " . $_SESSION['firstName'];
		}
		?>
	</h2>

	<h2>
		<?php
		if(!isset($_GET['error']) && isset($_SESSION['password'])) {
			echo "Password: " . $_SESSION['password'];
		}
		?>
	</h2>

</body>
</html>
```

### handleForm.php
```php
<?php 
session_start();

if(isset($_SESSION['firstName'])) {
	$loggedInUser = $_SESSION['firstName'];
	header("Location: index.php?error=already_logged_in&user=$loggedInUser");
	exit();
}

if(isset($_POST['submitBtn'])) {

	$firstName = $_POST['firstName'];

	$password = md5($_POST['password']);

	$_SESSION['firstName'] = $firstName;
	$_SESSION['password'] = $password;

	header('Location: index.php');
	exit();
}
?>
```

### unset.php
```php
<?php  
session_start();
session_unset();
header('Location: index.php'); 
?>
```
