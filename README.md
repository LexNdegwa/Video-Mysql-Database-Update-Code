Video-Mysql-Database-Update-Code
================================
<!DOCTYPE html PUBLIC “-//W3C//DTD XHTML 1.0 Transitional//EN” “http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd”>
<html xmlns=”http://www.w3.org/1999/xhtml”>
<head>
<meta http-equiv=”Content-Type” content=”text/html; charset=utf-8″ />
<title>Untitled Document</title>
</head>

<body>
<table>
<form action=”upload.php” method=”post” enctype=”multipart/form-data”>
<tr><td><label>Video Name : </label></td><td><input type=”text” name=”vname”/></td></tr>
<tr><td><label>Category : </label></td><td><input type=”text” name=”cat”/></td></tr>
<tr><td><label>Keywords : </label></td><td><input type=”text” name=”kwd”/></td></tr>
<tr><td><label>Upload file: </label></td><td><input type=”file” name=”uploaded” /></td></tr>
<tr><td></td><td><input type=”submit” value=”Upload” /></td></tr>
</form>
</tr>
</table>
<?php
$videoname = $_POST['vname'];
$category = $_POST['cat'];
$keyword = $_POST['kwd'];
$path = $_POST['uploaded'];
$target = “C:/xampp/htdocs/wordpress/wp-content/themes/metube-theme/upload/”;
$target = $target . basename($_FILES['uploaded']['name']);

if(empty($videoname) || empty($category) || empty($keyword)){
echo “<b>Please fill all field then try agian</b>”;
}else{
if(move_uploaded_file($_FILES['uploaded']['tmp_name'], $target)){
echo “The file (“. basename($_FILES['uploaded']['name']). “) has been upload”; 
}
else{
echo “Sorry, there was a problem uploading your file.”;
}
echo “<br/>”;
}
?>

<?php
$path = str_replace(“C:/xampp/htdocs”,”http://localhost”,$target);
$query = “INSERT INTO videos(videoname, category, keywords, path)”;
$query .= “VALUE (‘$videoname’, ‘$category’, ‘$keyword’, ‘$path’)”;
$result = mysql_query($query);

?>
</body>
</html>