<!DOCTYPEhtml>
<html>
<body>
<?php
$conn = mysqli_connect("localhost", "root", "3480", "db");
if($conn === false){
    die("ERROR: Could not connect. " . mysqli_connect_error());
}
// Attempt select query execution with order by clause
$sql = "create table proj( id int(6) AUTO_INCREMENT PRIMARY KEY,first_name varchar(22),last_name varchar(22),email varchar(22));";
$sql .= "insert into proj (id,first_name,last_name,email) values (1,'Arun','Sharma','a@gmail.com'), (2,'Bharat','Sharma','b@gmail.com'), (3,'Nitin','Sharma','n@gmail.com')";
if (mysqli_multi_query($conn, $sql)){
        echo "Table Created Succesfully";
} else{
        echo "Error crearting table" . mysqli_error($conn);
}
mysqli_close($conn);
?>
<?php
$conn = mysqli_connect("localhost", "root", "3480", "db");
if($conn === false){
    die("ERROR: Could not connect. " . mysqli_connect_error());
}
$query = "SELECT * FROM proj ORDER BY first_name DESC";
if($result = mysqli_query($conn, $query)){      
    if(mysqli_num_rows($result) > 0){
        echo "<table>";
            echo "<tr>";
                echo "<th>Id</th>";
                echo "<th>Firstname</th>";
                echo "<th>Lastname</th>";
                echo "<th>Email</th>";
            echo "</tr>";
        while($row = mysqli_fetch_array($result)){
            echo "<tr>";
                echo "<td>" . $row['id'] . "</td>";
                echo "<td>" . $row['first_name'] . "</td>";
                echo "<td>" . $row['last_name'] . "</td>";
                echo "<td>" . $row['email'] . "</td>";
            echo "</tr>";
        }
        echo "</table>"; 
        mysqli_free_result($result);
    } else{
        echo "No records matching your query were found.";
    }
} else{
    echo "ERROR: Could not able to execute $sql. " . mysqli_error($conn);
}
mysqli_close($conn);
?>
</body>
</html>

