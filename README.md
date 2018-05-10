<html>
<head>
<style>
.error {color: #FF0000;}

</style>
</head>

<body>
<?php
error_reporting(0);
?>
<?php 
// define variables
$nameErr = $emailErr = $passErr = $mobileErr = $websiteErr = $genderErr = "";
$name = $email = $pass = $mobile = $website = $gender = $selected = "";
if(isset($_POST['submit'])){
if (empty($_POST["name"])) {
    $nameErr = "Name is required";
  } else {
    $name = test_input($_POST["name"]);
    // check if name only contains letters and whitespace
    if (!preg_match("/^[a-zA-Z ]*$/",$name)) {
      $nameErr = "Only letters and white space allowed"; 
    }
  }
 if (empty($_POST["email"])) {
    $emailErr = "Email is required";
  } else {
    $email = test_input($_POST["email"]);
    // check if e-mail address is well-formed
    if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
      $emailErr = "Invalid email format"; 
    }
  }
if (empty($_POST["website"])) {
    $website = "";
  } else {
    $website = test_input($_POST["website"]);
    // check if URL address syntax is valid.
    if (!preg_match("/\b(?:(?:https?|ftp):\/\/|www\.)[-a-z0-9+&@#\/%?=~_|!:,.;]*[-a-z0-9+&@#\/%=~_|]/i",$website)) {
      $websiteErr = "Invalid URL"; 
    }
  }
if (empty($_POST["mobile"])) {
    $mobileErr = "Mobile is required";
  } else {
    $mobile = test_input($_POST["mobile"]);
	if(!preg_match('/^\+?([0-9]{1,4})\)?[-. ]?([0-9]{10})$/', $mobile) ) {
     $mobileErr = "Please enter a valid phone number";
} 
  
  }
  
		  
if (empty($_POST["pass"])) {
    $passErr = "Password is required";
  } else {
    $pass = test_input($_POST["pass"]);
  }
  
if (empty($_POST["gender"])) {
    $genderErr = "Gender is required";
  } else {
    $gender = test_input($_POST["gender"]);
  }
if(!empty($_POST['check_list'])){
// Loop to store and display values of individual checked checkbox.
foreach($_POST['check_list'] as $selected){
echo $selected."</br>";
}
}

}

function test_input($data) {
  $data = trim($data);
  $data = stripslashes($data);
  $data = htmlspecialchars($data);
  return $data;
}



?>





<?php
echo $name;
echo "<br>";
echo $email;
echo "<br>";
echo $pass;
echo "<br>";
echo $mobile;
echo "<br>";
echo $website;
echo "<br>";
echo $gender;


?>
<h2>Form Validation with PHP.</h2>

<span class="error">* required field </span></p>
<form action="" method="POST">
    Name: <input type="text" name="name" value="<?php echo $name; ?> ">
      <span class="error">* <?php echo $nameErr;?></span><br><br>
    Email: <input type="text" name="email" value="<?php echo $email; ?>">
      <span class="error">* <?php echo $emailErr;?></span><br><br>
    Password: <input type="password" name="pass" value="<?php echo $pass; ?>">
      <span class="error">* <?php echo $passErr;?></span><br><br>
    Mobile: <input type="text" name="mobile" value="<?php echo $mobile; ?>">
      <span class="error">* <?php echo $mobileErr;?></span><br><br>
    Website: <input type="text" name="website" value="<?php echo $website; ?>"><br><br>
     <span class="error"><?php echo $websiteErr;?></span>
	Gender:
	 <input type="radio" name="gender" <?php if (isset($gender) && $gender=="female") echo "checked"; ?> value="female">Female
	 <input type="radio" name="gender" <?php if (isset($gender) && $gender=="Male") echo "checked"; ?> value="male">Male
	 <input type="radio" name="gender" <?php if (isset($gender) && $gender=="other") echo "checked"; ?> value="other">Other
	 <span class="error">* <?php echo $genderErr;?></span>
	 <br><br>
	CheckBox:
	<br>
	 <input type="checkbox" name="check_list[]" value="C/C++"><label>C/C++</label><br/>
     <input type="checkbox" name="check_list[]" value="Java"><label>Java</label><br/>
     <input type="checkbox" name="check_list[]" value="PHP"><label>PHP</label><br/>
	 <input type="submit" name="submit" value="Submit">
     
</form>

</body>

</html>
