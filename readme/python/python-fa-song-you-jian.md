# python发送邮件

```
#注：
sender = 'from@fromdomain.com'
receivers = ['to@todomain.com']
message = """From: From Person <from@fromdomain.com>
To: To Person <to@todomain.com>
Subject: SMTP e-mail test
 
This is a test e-mail message.
"""
 
try:
   smtpObj = smtplib.SMTP('localhost')
   smtpObj.sendmail(sender, receivers, message)         
   print "Successfully sent email"
except SMTPException:
   print "Error: unable to send email"
#文件形式的邮件﻿​ 
```

```
#!/usr/bin/env python3  
#coding: utf-8  
import smtplib  
from email.mime.text import MIMEText  
from email.header import Header  
 
sender = '***'  
receiver = '***'  
subject = 'python email test'  
smtpserver = 'smtp.163.com'  
username = '***'  
password = '***'  
 
msg = MIMEText('你好','text','utf-8')#中文需参数‘utf-8’，单字节字符不需要  
msg['Subject'] = Header(subject, 'utf-8')  
 
smtp = smtplib.SMTP()  
smtp.connect('smtp.163.com')  
smtp.login(username, password)  
smtp.sendmail(sender, receiver, msg.as_string())  
smtp.quit()  
 
HTML形式的邮件
 
#!/usr/bin/env python3  
#coding: utf-8  
import smtplib  
from email.mime.text import MIMEText  
 
sender = '***'  
receiver = '***'  
subject = 'python email test'  
smtpserver = 'smtp.163.com'  
username = '***'  
password = '***'  
 
msg = MIMEText('<html><h1>你好</h1></html>','html','utf-8')  
 
msg['Subject'] = subject  
 
smtp = smtplib.SMTP()  
smtp.connect('smtp.163.com')  
smtp.login(username, password)  
smtp.sendmail(sender, receiver, msg.as_string())  
smtp.quit()  
 
带图片的HTML邮件
 
#!/usr/bin/env python3  
#coding: utf-8  
import smtplib  
from email.mime.multipart import MIMEMultipart  
from email.mime.text import MIMEText  
from email.mime.image import MIMEImage  
 
sender = '***'  
receiver = '***'  
subject = 'python email test'  
smtpserver = 'smtp.163.com'  
username = '***'  
password = '***'  
 
msgRoot = MIMEMultipart('related')  
msgRoot['Subject'] = 'test message'  
 
msgText = MIMEText('<b>Some <i>HTML</i> text</b> and an image.<br><img src="cid:image1"><br>good!','html','utf-8')  
msgRoot.attach(msgText)  
 
fp = open('h:\\python\\1.jpg', 'rb')  
msgImage = MIMEImage(fp.read())  
fp.close()  
 
msgImage.add_header('Content-ID', '<image1>')  
msgRoot.attach(msgImage)  
 
smtp = smtplib.SMTP()  
smtp.connect('smtp.163.com')  
smtp.login(username, password)  
smtp.sendmail(sender, receiver, msgRoot.as_string())  
smtp.quit()  
 
带附件的邮件
 
#!/usr/bin/env python3  
#coding: utf-8  
import smtplib  
from email.mime.multipart import MIMEMultipart  
from email.mime.text import MIMEText  
from email.mime.image import MIMEImage  
 
sender = '***'  
receiver = '***'  
subject = 'python email test'  
smtpserver = 'smtp.163.com'  
username = '***'  
password = '***'  
 
msgRoot = MIMEMultipart('related')  
msgRoot['Subject'] = 'test message'  
 
#构造附件  
att = MIMEText(open('h:\\python\\1.jpg', 'rb').read(), 'base64', 'utf-8')  
att["Content-Type"] = 'application/octet-stream'  
att["Content-Disposition"] = 'attachment; filename="1.jpg"'  
msgRoot.attach(att)  
 
smtp = smtplib.SMTP()  
smtp.connect('smtp.163.com')  
smtp.login(username, password)  
smtp.sendmail(sender, receiver, msgRoot.as_string())  
smtp.quit()  
 
群邮件
 
#!/usr/bin/env python3  
#coding: utf-8  
import smtplib  
from email.mime.text import MIMEText  
 
sender = '***'  
receiver = ['***','****',……]  
subject = 'python email test'  
smtpserver = 'smtp.163.com'  
username = '***'  
password = '***'  
 
msg = MIMEText('你好','text','utf-8')  
 
msg['Subject'] = subject  
 
smtp = smtplib.SMTP()  
smtp.connect('smtp.163.com')  
smtp.login(username, password)  
smtp.sendmail(sender, receiver, msg.as_string())  
smtp.quit()  
 
各种元素都包含的邮件
 
#!/usr/bin/env python3  
#coding: utf-8  
import smtplib  
from email.mime.multipart import MIMEMultipart  
from email.mime.text import MIMEText  
from email.mime.image import MIMEImage  
 
sender = '***'  
receiver = '***'  
subject = 'python email test'  
smtpserver = 'smtp.163.com'  
username = '***'  
password = '***'  
 
# Create message container - the correct MIME type is multipart/alternative.  
msg = MIMEMultipart('alternative')  
msg['Subject'] = "Link"  
 
# Create the body of the message (a plain-text and an HTML version).  
text = "Hi!\nHow are you?\nHere is the link you wanted:\nhttp://www.python.org"  
html = """\ 
<html> 
  <head></head> 
  <body> 
    <p>Hi!<br> 
       How are you?<br> 
       Here is the <a href="http://www.python.org">link</a> you wanted. 
    </p> 
  </body> 
</html> 
"""  
 
# Record the MIME types of both parts - text/plain and text/html.  
part1 = MIMEText(text, 'plain')  
part2 = MIMEText(html, 'html')  
 
# Attach parts into message container.  
# According to RFC 2046, the last part of a multipart message, in this case  
# the HTML message, is best and preferred.  
msg.attach(part1)  
msg.attach(part2)  
#构造附件  
att = MIMEText(open('h:\\python\\1.jpg', 'rb').read(), 'base64', 'utf-8')  
att["Content-Type"] = 'application/octet-stream'  
att["Content-Disposition"] = 'attachment; filename="1.jpg"'  
msg.attach(att)  
 
smtp = smtplib.SMTP()  
smtp.connect('smtp.163.com')  
smtp.login(username, password)  
smtp.sendmail(sender, receiver, msg.as_string())  
smtp.quit()  
 
基于SSL的邮件
 
#!/usr/bin/env python3  
#coding: utf-8  
import smtplib  
from email.mime.text import MIMEText  
from email.header import Header  
sender = '***'  
receiver = '***'  
subject = 'python email test'  
smtpserver = 'smtp.163.com'  
username = '***'  
password = '***'  
 
msg = MIMEText('你好','text','utf-8')#中文需参数‘utf-8’，单字节字符不需要  
msg['Subject'] = Header(subject, 'utf-8')  
 
smtp = smtplib.SMTP()  
smtp.connect('smtp.163.com')  
smtp.ehlo()  
smtp.starttls()  
smtp.ehlo()  
smtp.set_debuglevel(1)  
smtp.login(username, password)  
smtp.sendmail(sender, receiver, msg.as_string())  
smtp.quit()  
 
文件形式的邮件
 
#!/usr/bin/env python3  
#coding: utf-8  
import smtplib  
from email.mime.text import MIMEText  
from email.header import Header  
 
sender = '***'  
receiver = '***'  
subject = 'python email test'  
smtpserver = 'smtp.163.com'  
username = '***'  
password = '***'  
 
msg = MIMEText('你好','text','utf-8')#中文需参数‘utf-8’，单字节字符不需要  
msg['Subject'] = Header(subject, 'utf-8')  
 
smtp = smtplib.SMTP()  
smtp.connect('smtp.163.com')  
smtp.login(username, password)  
smtp.sendmail(sender, receiver, msg.as_string())  
smtp.quit()  
 
HTML形式的邮件
 
#!/usr/bin/env python3  
#coding: utf-8  
import smtplib  
from email.mime.text import MIMEText  
 
sender = '***'  
receiver = '***'  
subject = 'python email test'  
smtpserver = 'smtp.163.com'  
username = '***'  
password = '***'  
 
msg = MIMEText('<html><h1>你好</h1></html>','html','utf-8')  
 
msg['Subject'] = subject  
 
smtp = smtplib.SMTP()  
smtp.connect('smtp.163.com')  
smtp.login(username, password)  
smtp.sendmail(sender, receiver, msg.as_string())  
smtp.quit()  
 
带图片的HTML邮件
 
#!/usr/bin/env python3  
#coding: utf-8  
import smtplib  
from email.mime.multipart import MIMEMultipart  
from email.mime.text import MIMEText  
from email.mime.image import MIMEImage  
 
sender = '***'  
receiver = '***'  
subject = 'python email test'  
smtpserver = 'smtp.163.com'  
username = '***'  
password = '***'  
 
msgRoot = MIMEMultipart('related')  
msgRoot['Subject'] = 'test message'  
 
msgText = MIMEText('<b>Some <i>HTML</i> text</b> and an image.<br><img src="cid:image1"><br>good!','html','utf-8')  
msgRoot.attach(msgText)  
 
fp = open('h:\\python\\1.jpg', 'rb')  
msgImage = MIMEImage(fp.read())  
fp.close()  
 
msgImage.add_header('Content-ID', '<image1>')  
msgRoot.attach(msgImage)  
 
smtp = smtplib.SMTP()  
smtp.connect('smtp.163.com')  
smtp.login(username, password)  
smtp.sendmail(sender, receiver, msgRoot.as_string())  
smtp.quit()  
带附件的邮件
#!/usr/bin/env python3  
#coding: utf-8  
import smtplib  
from email.mime.multipart import MIMEMultipart  
from email.mime.text import MIMEText  
from email.mime.image import MIMEImage  
 
sender = '***'  
receiver = '***'  
subject = 'python email test'  
smtpserver = 'smtp.163.com'  
username = '***'  
password = '***'  
 
msgRoot = MIMEMultipart('related')  
msgRoot['Subject'] = 'test message'  
 
#构造附件  
att = MIMEText(open('h:\\python\\1.jpg', 'rb').read(), 'base64', 'utf-8')  
att["Content-Type"] = 'application/octet-stream'  
att["Content-Disposition"] = 'attachment; filename="1.jpg"'  
msgRoot.attach(att)  
 
smtp = smtplib.SMTP()  
smtp.connect('smtp.163.com')  
smtp.login(username, password)  
smtp.sendmail(sender, receiver, msgRoot.as_string())  
smtp.quit()  
群邮件
 
#!/usr/bin/env python3  
#coding: utf-8  
import smtplib  
from email.mime.text import MIMEText  
 
sender = '***'  
receiver = ['***','****',……]  
subject = 'python email test'  
smtpserver = 'smtp.163.com'  
username = '***'  
password = '***'  
 
msg = MIMEText('你好','text','utf-8')  
 
msg['Subject'] = subject  
 
smtp = smtplib.SMTP()  
smtp.connect('smtp.163.com')  
smtp.login(username, password)  
smtp.sendmail(sender, receiver, msg.as_string())  
smtp.quit()  
各种元素都包含的邮件
 
#!/usr/bin/env python3  
#coding: utf-8  
import smtplib  
from email.mime.multipart import MIMEMultipart  
from email.mime.text import MIMEText  
from email.mime.image import MIMEImage  
 
sender = '***'  
receiver = '***'  
subject = 'python email test'  
smtpserver = 'smtp.163.com'  
username = '***'  
password = '***'  
 
# Create message container - the correct MIME type is multipart/alternative.  
msg = MIMEMultipart('alternative')  
msg['Subject'] = "Link"  
 
# Create the body of the message (a plain-text and an HTML version).  
text = "Hi!\nHow are you?\nHere is the link you wanted:\nhttp://www.python.org"  
html = """\ 
<html> 
  <head></head> 
  <body> 
    <p>Hi!<br> 
       How are you?<br> 
       Here is the <a href="http://www.python.org">link</a> you wanted. 
    </p> 
  </body> 
</html> 
"""  
 
# Record the MIME types of both parts - text/plain and text/html.  
part1 = MIMEText(text, 'plain')  
part2 = MIMEText(html, 'html')  
 
# Attach parts into message container.  
# According to RFC 2046, the last part of a multipart message, in this case  
# the HTML message, is best and preferred.  
msg.attach(part1)  
msg.attach(part2)  
#构造附件  
att = MIMEText(open('h:\\python\\1.jpg', 'rb').read(), 'base64', 'utf-8')  
att["Content-Type"] = 'application/octet-stream'  
att["Content-Disposition"] = 'attachment; filename="1.jpg"'  
msg.attach(att)  
 
smtp = smtplib.SMTP()  
smtp.connect('smtp.163.com')  
smtp.login(username, password)  
smtp.sendmail(sender, receiver, msg.as_string())  
smtp.quit()  
 
基于SSL的邮件
 
#!/usr/bin/env python3  
#coding: utf-8  
import smtplib  
from email.mime.text import MIMEText  
from email.header import Header  
sender = '***'  
receiver = '***'  
subject = 'python email test'  
smtpserver = 'smtp.163.com'  
username = '***'  
password = '***'  
 
msg = MIMEText('你好','text','utf-8')#中文需参数‘utf-8’，单字节字符不需要  
msg['Subject'] = Header(subject, 'utf-8')  
 
smtp = smtplib.SMTP()  
smtp.connect('smtp.163.com')  
smtp.ehlo()  
smtp.starttls()  
smtp.ehlo()  
smtp.set_debuglevel(1)  
smtp.login(username, password)  
smtp.sendmail(sender, receiver, msg.as_string())  
smtp.quit() 
 
 
 
 
 
import smtplib 
from email.mime.text import MIMEText 
mailto_list=["YYY@YYY.com"] 
mail_host="smtp.XXX.com"  #设置服务器
mail_user="XXX"    #用户名
mail_pass="XXXX"   #口令 
mail_postfix="XXX.com"  #发件箱的后缀
 
def send_mail(to_list,sub,content):  #to_list：收件人；sub：主题；content：邮件内容
    me="hello"+"<"+mail_user+"@"+mail_postfix+">"   #这里的hello可以任意设置，收到信后，将按照设置显示
    msg = MIMEText(content,_subtype='html',_charset='gb2312')    #创建一个实例，这里设置为html格式邮件
    msg['Subject'] = sub    #设置主题
    msg['From'] = me 
    msg['To'] = ";".join(to_list) 
    try: 
        s = smtplib.SMTP() 
        s.connect(mail_host)  #连接smtp服务器
        s.login(mail_user,mail_pass)  #登陆服务器
        s.sendmail(me, to_list, msg.as_string())  #发送邮件
        s.close() 
        return True 
    except Exception, e: 
        print str(e) 
        return False 
if __name__ == '__main__': 
    if send_mail(mailto_list,"hello","<a href='http://www.cnblogs.com/xiaowuyi'>小五义</a>"): 
        print "发送成功" 
    else: 
        print "发送失败" ﻿​
```
