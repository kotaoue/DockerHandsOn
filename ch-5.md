```ShellSession
$ cd ~/ghq/github.com/kotaoue/DockerHandsOn/
$ docker run -dit --name web01 -p 8080:80 httpd:2.4
eede17eeb130e31d01e94fa943dbb4389d974476602bdbb33999b80444ea46e6
$ docker run -dit --name web02 -p 8081:80 httpd:2.4
9526da19310dacc9d1cbae35580b55468d6ef9b9a10c39b635c8501063b01a71
$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
9526da19310d        httpd:2.4           "httpd-foreground"   2 seconds ago       Up 2 seconds        0.0.0.0:8081->80/tcp   web02
eede17eeb130        httpd:2.4           "httpd-foreground"   16 seconds ago      Up 15 seconds       0.0.0.0:8080->80/tcp   web01
$ curl localhost:8080
<html><body><h1>It works!</h1></body></html>
$ curl localhost:8081
<html><body><h1>It works!</h1></body></html>

$ cp index.html index2.html 
$ vim index2.html 
$ docker cp index.html web01:/usr/local/apache2/htdocs/index.html
$ curl localhost:8080
<html>
<head>
<title>index.html</title>
</head>
<body>
I'm index.html
</body>
</html>

$ docker exec -it web01 /bin/bash
root@eede17eeb130:/usr/local/apache2# ls
bin  build  cgi-bin  conf  error  htdocs  icons  include  logs	modules
root@eede17eeb130:/usr/local/apache2# ls -la /usr/local/apache2/htdocs/
total 16
drwxr-xr-x 1 root     root     4096 Aug 10 23:22 .
drwxr-xr-x 1 www-data www-data 4096 Aug  5 23:21 ..
-rw-r--r-- 1      502 dialout    86 Aug  9 10:31 index.html
root@eede17eeb130:/usr/local/apache2# cat /usr/local/apache2/htdocs/index.html 
<html>
<head>
<title>index.html</title>
</head>
<body>
I'm index.html
</body>
</html>
root@eede17eeb130:/usr/local/apache2# exit
exit

$ docker cp index2.html web02:/usr/local/apache2/htdocs/index.html
$ curl localhost:8081
<html>
<head>
<title>index.html</title>
</head>
<body>
I'm index2.html
</body>
</html>
```