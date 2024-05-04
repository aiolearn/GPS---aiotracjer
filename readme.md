# GPS - aiotracker

In this project, we have written a car tracking program that can receive the coordinates from the tracking device and display it on the map.

## Skills

Htmkl / css / js / php / mysql

## Usage

connect to database

```php
$db = mysqli_connect('aiolearnfamily.com','aiolear3_admingps','gps1402@!','aiolear3_gps');
date_default_timezone_set("Asia/Tehran");
mysqli_set_charset($db, 'utf8');
```

Register section
```php
require('database.php');

$username='';
$mobile='';
$namefull='';
$password='';

if (isset($_POST['username'])){

    $username=$_POST['username'];
    $mobile=$_POST['mobile'];
    $namefull=$_POST['namefull'];
    $password=$_POST['password'];

    $sql= mysqli_query($db , 
"insert into users (username,mobile,namefull,pass) values
('$username','$mobile','$namefull','$password')" );
}
```

login section

```php
require('database.php');

$username='';  
$password='';

if (isset($_POST['username'])){

    $username=$_POST['username'];
    $password=$_POST['password']; 

    $sql= mysqli_query($db ,
    "select * from users where (username='$username' or mobile='$username') and pass='$password';" );

    $login=0;

    if ($row=mysqli_fetch_assoc($sql)){
        $login=1;

        setcookie('username', $row['username'], time() + (86400 * 30), "/");
        setcookie('namefull', $row['namefull'], time() + (86400 * 30), "/");
        setcookie('userid', $row['id'], time() + (86400 * 30), "/");
        echo '<meta http-equiv="refresh" content="0; URL=\'index.php\'" /> ';
    }else{
        echo '<div style="direction: rtl;" class="alert alert-danger" role="alert">
            نام کاربری یا رمز عبور اشتباه است!
        </div>';
    }
}
```


Display the location of the device on the map

```javascript
function myMap() {
    var gpsx=0;
    var gpsy=0;
    <?php
    $sql=mysqli_query($db,"
        select * from device_log order by id desc limit 1;
    ");
    if($row=mysqli_fetch_assoc($sql)){
        echo '
        gpsx= '.$row['gpsx'].';
        gpsy= '.$row['gpsy'].';
        ';
    }
    ?>
    var myCenter = new google.maps.LatLng(gpsx, gpsy);  
    var mapCanvas = document.getElementById("map");
    var mapOptions = {
      center: myCenter, 
      zoom: 11,
      mapTypeId: google.maps.MapTypeId.ROADMAP
    }
      
    var map = new google.maps.Map(mapCanvas, mapOptions); 
    google.maps.event.addListener(map,'click',function() {click1();});
    
    var p1 = new google.maps.LatLng(gpsx, gpsy);
    var marker = new google.maps.Marker({position: p1,  icon: { url: "images/loc.png", scaledSize: new 
google.maps.Size(33, 50)}  });
 
    marker.setMap(map);
    
    var infoWindow = new google.maps.InfoWindow();
    
    google.maps.event.addListener(marker, 'click', function () {
        var markerContent = '<button> click </button> Majid Tejenjari <br><br> توضیحات دلخواه';
        infoWindow.setContent(markerContent);
        infoWindow.open(map, this);
    });
}
    
function click1(){
}
```


## Result
This project was written by Majid Tajanjari and the Aiolearn team, and we need your support!❤️

# GPS - aiotracker

در این پروژه یک برنامه ردیابی خودرو نوشته ایم که می تواند مختصات را از دستگاه ردیاب دریافت کرده و روی نقشه نمایش دهد.

## مهارت ها

Htmkl / css / js / php / mysql

## نحوه استفاده

اتصال به دیتابیس

```php
$db = mysqli_connect('aiolearnfamily.com','aiolear3_admingps','gps1402@!','aiolear3_gps');
date_default_timezone_set("Asia/Tehran");
mysqli_set_charset($db, 'utf8');
```

بخش ثبت نام

```php
require('database.php');

$username='';
$mobile='';
$namefull='';
$password='';

if (isset($_POST['username'])){

    $username=$_POST['username'];
    $mobile=$_POST['mobile'];
    $namefull=$_POST['namefull'];
    $password=$_POST['password'];

    $sql= mysqli_query($db , 
"insert into users (username,mobile,namefull,pass) values
('$username','$mobile','$namefull','$password')" );
}
```

بخش ورود

```php
require('database.php');

$username='';  
$password='';

if (isset($_POST['username'])){

    $username=$_POST['username'];
    $password=$_POST['password']; 

    $sql= mysqli_query($db ,
    "select * from users where (username='$username' or mobile='$username') and pass='$password';" );

    $login=0;

    if ($row=mysqli_fetch_assoc($sql)){
        $login=1;

        setcookie('username', $row['username'], time() + (86400 * 30), "/");
        setcookie('namefull', $row['namefull'], time() + (86400 * 30), "/");
        setcookie('userid', $row['id'], time() + (86400 * 30), "/");
        echo '<meta http-equiv="refresh" content="0; URL=\'index.php\'" /> ';
    }else{
        echo '<div style="direction: rtl;" class="alert alert-danger" role="alert">
            نام کاربری یا رمز عبور اشتباه است!
        </div>';
    }
}
```


نمایش موقعیت دستگاه در نقشه

```javascript
function myMap() {
    var gpsx=0;
    var gpsy=0;
    <?php
    $sql=mysqli_query($db,"
        select * from device_log order by id desc limit 1;
    ");
    if($row=mysqli_fetch_assoc($sql)){
        echo '
        gpsx= '.$row['gpsx'].';
        gpsy= '.$row['gpsy'].';
        ';
    }
    ?>
    var myCenter = new google.maps.LatLng(gpsx, gpsy);  
    var mapCanvas = document.getElementById("map");
    var mapOptions = {
      center: myCenter, 
      zoom: 11,
      mapTypeId: google.maps.MapTypeId.ROADMAP
    }
      
    var map = new google.maps.Map(mapCanvas, mapOptions); 
    google.maps.event.addListener(map,'click',function() {click1();});
    
    var p1 = new google.maps.LatLng(gpsx, gpsy);
    var marker = new google.maps.Marker({position: p1,  icon: { url: "images/loc.png", scaledSize: new 
google.maps.Size(33, 50)}  });
 
    marker.setMap(map);
    
    var infoWindow = new google.maps.InfoWindow();
    
    google.maps.event.addListener(marker, 'click', function () {
        var markerContent = '<button> click </button> Majid Tejenjari <br><br> توضیحات دلخواه';
        infoWindow.setContent(markerContent);
        infoWindow.open(map, this);
    });
}
    
function click1(){
}
```


## نتیجه

این پروژه توسط مجید تجن جاری و تیم Aiolearn نوشته شده است و ما به حمایت شما نیازمندیم!❤️