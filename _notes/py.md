python自带两个模块，smtplib和email，只需import即可使用。

smtplib模块主要负责发送邮件，，连接邮箱服务器，登录邮箱，发送邮件（有发件人，收信人，邮件内容）
```
  import smtplib

  smtp = smtplib.SMTP() 
  smtp.connect('smtp.163.com',25) 
  smtp.login(username, password) 
  smtp.sendmail(sender, receiver, msg.as_string()) 
  smtp.quit()
```
msg.as_string() 是将msg(MIMEText对象orMIMEMultipart对象)变为str。

**MINE** stands for "Multipurpose Internet Mail Extensions"


email模块主要负责构造邮件。指的是邮箱页面显示的一些构造，如发件人，收件人，主题，正文，附件等。

构造一个邮件对象就是一个Message对象，如果构造一个MIMEText对象，就表示一个文本邮件对象，如果构造一个MIMEImage对象，就表示一个作为附件的图片，要把多个对象组合起来，就用MIMEMultipart对象，而MIMEBase可以表示任何对象
```
  from email.mime.multipart import MIMEMultipart    
  from email.mime.text import MIMEText    
  from email.mime.image import MIMEImage
```
它们的继承关系如下：
```
  +- MIMEBase
   +- MIMEMultipart
   +- MIMENonMultipart
      +- MIMEMessage
      +- MIMEText
      +- MIMEImage
```
常见的multipart类型有三种：multipart/alternative, multipart/related和multipart/mixed。

邮件类型为"multipart/alternative"的邮件包括纯文本正文（text/plain）和超文本正文（text/html）。

邮件类型为"multipart/related"的邮件正文中包括图片，声音等内嵌资源。

邮件类型为"multipart/mixed"的邮件包含附件。向上兼容，如果一个邮件有纯文本正文，超文本正文，内嵌资源，附件，则选择mixed类型。


如果只有一个html超文本正文或者plain普通文本正文的话，一般msg的类型可以是MIMEText；如果是多个的话，就都添加到MIMEMultipart，msg类型就变为MIMEMultipart。

