### index.php
```php
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Discriminant of a Quadratic Equation</title>
</head>
<body>
<h1>Discriminant of a Quadratic Equation</h1>
	<form action="testGet.php" method="GET">
    
		<p>A: <input type="text" placeholder="Value of a here" name="num1"></p>
		<p>B: <input type="text" placeholder="Value of b here" name="num2"></p>
        <p>C: <input type="text" placeholder="Value of c here" name="num3"></p>

		<p><input type="submit" value="Submit" name="getDiscriminant"></p>
	</form>
</body>
</html>
```

### getTest.php
```php
<?php  
if(isset($_GET['getDiscriminant'])) {

	$num1 = $_GET['num1'];
	$num2 = $_GET['num2'];
    $num3 = $_GET['num3'];

	$discriminant = $num2*$num2 - 4*$num1*$num3;

	echo "<h2>" . $discriminant . "</h2>";
}
?>
```
