---
title: php处理postgresql图片
categories:
  - 未分类
date: 2020-09-10 14:49:37
tags:
---
#### 连接pgsql数据库

```
$host        = "host=xxx";
$port        = "port=5432";
$dbname      = "dbname=xxx";
$credentials = "user=postgres password=xxx";

$db = pg_connect( "$host $port $dbname $credentials"  );
if(!$db){
  echo "Error : Unable to open database\n";
} else {
  echo "Opened database successfully\n";
}
```
#### 查询数据库输出图片

##### 方法一 base64格式
```
$sql =  "SELECT id,encode(picture, 'BASE64') as picture FROM water_flow_pictures_data WHERE id=".$_GET['imgid'];

$ret = pg_query($db, $sql);
if(!$ret){
  echo pg_last_error($db);
  exit;
}
while($row = pg_fetch_row($ret)){
  // 方法一
  echo '<img src="data:image/jpg;base64,' . $row[1] .'"/>';
}
```
##### 方法二 
```
$sql =  "SELECT id,picture FROM water_flow_pictures_data WHERE id=".$_GET['imgid'];

$ret = pg_query($db, $sql);
if(!$ret){
  echo pg_last_error($db);
  exit;
}
while($row = pg_fetch_row($ret)){
  // 方法二
  header("Content-Type: image/jpeg");
  echo pg_unescape_bytea($row[1]);
}
```

#### 缩放后输出（也可压缩质量）
```
// 获取原图属性
list($width, $height, $type, $attr) = getimagesizefromstring(pg_unescape_bytea($row[1]));
$newWidth = $_GET['width']?$_GET['width']: $width;
$newHeight = $height/$width * $newWidth;

$image =imagecreatefromstring(pg_unescape_bytea($row[1]));
$quality  = 0; // 图片输出质量，0 为最低


// Create a blank image and add some text
$im = imagecreatetruecolor($newWidth, $newHeight);
imagecopyresized($im,$image,0,0,0,0,$newWidth,$newHeight,$width,$height);
// $text_color = imagecolorallocate($im, 233, 14, 91);
// imagestring($im, 1, 5, 5,  'A Simple Text String', $text_color);

// Set the content type header - in this case image/jpeg
header('Content-Type: image/jpeg');

// Output the image
imagejpeg($im, null, $quality);

// Free up memory
imagedestroy($im);
```

#### 关闭数据库

```
pg_close($db);
```


#### 参考

https://www.php.net/manual/en/ref.image.php
https://www.runoob.com/php/php-image-gd.html