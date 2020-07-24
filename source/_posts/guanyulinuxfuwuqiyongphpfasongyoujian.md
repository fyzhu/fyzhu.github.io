---
title: 关于linux服务器用php发送邮件
url: 47.html
id: 47
categories:
  - 未分类
date: 2017-09-12 11:00:51
tags:
---

sendmail 
yum/apt-get install sendmail 
开启fsockopen函数 
服务器如何开启php的fsockopen函数？ 
https://jingyan.baidu.com/article/09ea3eded1d8bcc0aede3920.html 
yum install openssl openssl-devel   
端口：25 阿里云已经禁用25端口 请改为：465并把协议换成ssl 
详情查看文章：https://blog.hellozwh.com/?post=282

#### 一、PHP mail() 函数


PHP mail() 函数用于从脚本中发送电子邮件。 
```
<?php 
  $to = "someone@example.com"; 
  $subject = "Test mail"; 
  $message = "Hello! This is a simple email message."; 
  $from = "someonelse@example.com"; 
  $headers = "From: $from"; 
  mail($to,$subject,$message,$headers); 
  echo "Mail Sent."; 
?>  
```
#### 二、php利用smtp类轻松的发送电子邮件

```
<?php 
  require\_once "Smtp.class.php"; 
  //******************** 配置信息 ******************************** 
  $smtpserver = "smtp.126.com";//SMTP服务器 
  $smtpserverport =25;//SMTP服务器端口 
  $smtpusermail = "new2008oh@126.com";//SMTP服务器的用户邮箱 
  $smtpemailto = $\_POST\['toemail'\];//发送给谁 
  $smtpuser = "new2008oh";//SMTP服务器的用户帐号(或填写new2008oh@126.com，这项有些邮箱需要完整的) 
  $smtppass = "您的邮箱密码";//SMTP服务器的用户密码 
  $mailtitle = $\_POST\['title'\];//邮件主题 
  $mailcontent = "<h1>".$\_POST\['content'\]."</h1>";//邮件内容 
  $mailtype = "HTML";//邮件格式（HTML/TXT）,TXT为文本邮件 
  //************************ 配置信息 **************************** 
  $smtp = new Smtp($smtpserver,$smtpserverport,true,$smtpuser,$smtppass);// true 表示是否使用身份验证
  $smtp->debug = false;//是否显示发送的调试信息 
  $state = $smtp->sendmail($smtpemailto, $smtpusermail, $mailtitle, $mailcontent, $mailtype); 
  echo "<div style='width:300px; margin:36px auto;'>"; 
  if($state==""){ 
    echo "对不起，邮件发送失败！请检查邮箱填写是否有误。"; 
    echo "<a href='index.html'>点此返回</a>"; 
    exit(); 
  } 
  echo "恭喜！邮件发送成功！！"; 
  echo "<a href='index.html'>点此返回</a>"; 
  echo "</div>"; 
?>
```