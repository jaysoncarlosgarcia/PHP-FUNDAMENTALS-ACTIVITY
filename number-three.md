### index.php
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Order Form</title>
</head>
<body>
    <h1>Menu</h1>
    <table border="1">
        <tr>
            <th>Order</th>
            <th>Amount</th>
        </tr>
        <tr>
            <td>Burger</td>
            <td>50</td>
        </tr>
        <tr>
            <td>Fries</td>
            <td>75</td>
        </tr>
        <tr>
            <td>Steak</td>
            <td>150</td>
        </tr>
    </table>

    <form action="handleForm.php" method="POST">
        <p>
            <label for="order">Select an order:</label>
            <select name="order" id="order">
                <option value="Burger" data-price="50">Burger</option>
                <option value="Fries" data-price="75">Fries</option>
                <option value="Steak" data-price="150">Steak</option>
            </select>
        </p>
        <p>Quantity: <input type="number" name="quantity" required></p>
        <p>Cash: <input type="number" name="cash" required></p>
        <p><input type="submit" value="Submit"></p>
    </form>
</body>
</html>
```

### handleForm.php
```php
<?php
if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $order = $_POST['order'];
    $quantity = intval($_POST['quantity']);
    $cash = intval($_POST['cash']);
    
    $prices = [
        'Burger' => 50,
        'Fries' => 75,
        'Steak' => 150
    ];

    $totalPrice = $prices[$order] * $quantity;
    
    if ($cash < $totalPrice) {
        $errorMessage = "Sorry, balance not enough.";
        $isBalanceInsufficient = true;
    } else {
        $change = $cash - $totalPrice;
        $dateTime = date('m/d/Y h:i:s a', time());
        $isBalanceInsufficient = false;
    }
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Receipt</title>
</head>
<body>
    <?php if ($isBalanceInsufficient): ?>
        <h1><?php echo $errorMessage; ?></h1>
    <?php else: ?>
        <h1><center>RECEIPT</center></h1>
        <h1>Total Price: <?php echo $totalPrice; ?><h1>
        <h1>You Paid: <?php echo $cash; ?></h1>
        <h1>CHANGE: <?php echo $change; ?></h1>
        <h1><?php echo $dateTime; ?></h1>
    <?php endif; ?>
</body>
</html>
```
