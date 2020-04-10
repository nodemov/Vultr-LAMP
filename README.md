# Vultr-LAMP-SETUP-ONE-CLICK
This is education 
_______________________________________________________________________________________________________________________________
Vultr LAMP SETUP ONE-CLICK

The web document root is located at /var/www/html/. You can create .php or .html files in that folder. For example, uploading a PHP file to /var/www/html/donut.php would make the file accessible in your web browser at http://[SERVER_IP]/donut.php.


The VPS also runs a MySQL database server. You can connect to the database with the following command:

mysql -u root

The MySQL root password is saved on the VPS in /root/.my.cnf.

ssh root@ip 

terminal

Welcome to Ubuntu 18.04.4 LTS (GNU/Linux 4.15.0-88-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Fri Apr 10 13:01:51 UTC 2020

  System load:  0.31              Processes:           91
  Usage of /:   4.9% of 54.09GB   Users logged in:     0
  Memory usage: 15%               IP address for ens3: 139.180.223.7
  Swap usage:   0%


72 packages can be updated.
31 updates are security updates.

root@vultr:~# sudo apt-get update                  
root@vultr:~# sudo apt-get upgrade -y
root@vultr:~# ll
total 28
drwx------  4 root root 4096 Apr 10 13:00 ./
drwxr-xr-x 23 root root 4096 Mar 10 00:01 ../
-rw-r--r--  1 root root 3106 Apr  9  2018 .bashrc
drwx------  2 root root 4096 Mar 10 00:01 .cache/
drwx------  3 root root 4096 Mar 10 00:01 .gnupg/
-rw-r--r--  1 root root   44 Apr 10 13:00 .my.cnf
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
root@vultr:~# cat /root/.my.cnf
[client]
user=root
password=RWoE0vK7uj8W3vd
root@vultr:~# mysql -u root

root@vultr:~# cd /var/www/html/
root@vultr:/var/www/html# 
root@vultr:/var/www/html# touch donut.php
root@vultr:/var/www/html# vim donut.php 
root@vultr:/var/www/html# cat donut.php 
<?php

phpinfo();

?>
root@vultr:/var/www/html# ll
total 24
root@vultr:/var/www/html# vim connect.php
root@vultr:/var/www/html# cat connect.php 
<?php
$servername = "localhost";
$username = "root";
$password = "RWoE0vK7uj8W3vd";

// Create connection
$conn = new mysqli($servername, $username, $password);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully";
?>
root@vultr:/var/www/html# cd ..
root@vultr:/var/www# cd ..
root@vultr:/var# cd ..
root@vultr:/# cd ..
root@vultr:/# 
root@vultr:/# mysql -u root
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 5
Server version: 5.7.29-0ubuntu0.18.04.1 (Ubuntu)

Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> CREATE DATABASE testDB;
Query OK, 1 row affected (0.00 sec)
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| testDB             |
+--------------------+
5 rows in set (0.01 sec)

mysql> USE testDB;
Database changed
mysql> CREATE TABLE Persons (
    ->     PersonID int,
    ->     LastName varchar(255),
    ->     FirstName varchar(255),
    ->     Address varchar(255),
    ->     City varchar(255)
    -> );
Query OK, 0 rows affected (0.01 sec)

mysql> INSERT INTO Persons(PersonID,LastName,FirstName,Address,City) VALUES('1','Wijit','kanit','54/3','BKK');
Query OK, 1 row affected (0.03 sec)

mysql> select * from Persons;
+----------+----------+-----------+---------+------+
| PersonID | LastName | FirstName | Address | City |
+----------+----------+-----------+---------+------+
|        1 | Wijit    | kanit     | 54/3    | BKK  |
+----------+----------+-----------+---------+------+
1 row in set (0.00 sec)

mysql> ^C

^C
mysql> 
[2]+  Stopped                 mysql -u root
root@vultr:/# cd /var/www/html/

root@vultr:/var/www/html# nano connect.php 
root@vultr:/var/www/html# cat connect.php 
<?php
$servername = "localhost";
$username = "root";
$password = "RWoE0vK7uj8W3vd";
$db = "testDB";

// Create connection
$conn = new mysqli($servername, $username, $password,$db);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully";

$sql = "SELECT * FROM Persons";
$result = $conn->query($sql);
if ($result->num_rows > 0) {
    // output data of each row
    while($row = $result->fetch_assoc()) {
        echo "id: " . $row["PersonID"]. " - Name: " . $row["FirstName"]. " " . $row["LastName"]. "<br>";
    }
} else {
    echo "0 results";
}
$conn->close();


?>
root@vultr:/var/www/html# 
