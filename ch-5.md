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

$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
9526da19310d        httpd:2.4           "httpd-foreground"   8 minutes ago       Up 7 minutes        0.0.0.0:8081->80/tcp   web02
eede17eeb130        httpd:2.4           "httpd-foreground"   8 minutes ago       Up 8 minutes        0.0.0.0:8080->80/tcp   web01
$ docker stop web01
web01
$ curl localhost:8080
curl: (7) Failed to connect to localhost port 8080: Connection refused

$ docker start web01
web01
$ curl localhost:8080
<html>
<head>
<title>index.html</title>
</head>
<body>
I'm index.html
</body>
</html>
$ docker stop web01
web01
$ docker rm web01
web01
$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
9526da19310d        httpd:2.4           "httpd-foreground"   9 minutes ago       Up 9 minutes        0.0.0.0:8081->80/tcp   web02
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                     PORTS                                NAMES
9526da19310d        httpd:2.4           "httpd-foreground"       9 minutes ago       Up 9 minutes               0.0.0.0:8081->80/tcp                 web02
$ docker run -dit --name web01 -p 8080:80 httpd:2.4
5147dfe618f075fae6f269de409fee269aef907b96a7cc963265b4f89d238f1a
$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
5147dfe618f0        httpd:2.4           "httpd-foreground"   3 seconds ago       Up 2 seconds        0.0.0.0:8080->80/tcp   web01
9526da19310d        httpd:2.4           "httpd-foreground"   9 minutes ago       Up 9 minutes        0.0.0.0:8081->80/tcp   web02
$ curl localhost:8080
<html><body><h1>It works!</h1></body></html>

$ docker exec -it web01 /bin/bash 
root@5147dfe618f0:/usr/local/apache2# ls /usr/local/apache2/htdocs/
index.html
root@5147dfe618f0:/usr/local/apache2# cat /usr/local/apache2/htdocs/index.html 
<html><body><h1>It works!</h1></body></html>
root@5147dfe618f0:/usr/local/apache2# exit
exit

$ docker stop web01
web01
$ docker rm web01
web01

$ mkdir web01data
$ cp index.html web01data/index.html
$ vim web01data/index.html 

$ docker run -dit --name web01 -v web01data/:/usr/local/apache2/htdocs -p 9090:90 httpd:2.4
docker: Error response from daemon: create web01data/: "web01data/" includes invalid characters for a local volume name, only "[a-zA-Z0-9][a-zA-Z0-9_.-]" are allowed. If you intended to pass a host directory, use absolute path.
See 'docker run --help'.
$ docker run -dit --name web01 -v ./web01data/:/usr/local/apache2/htdocs -p 9090:90 httpd:2.4
docker: Error response from daemon: create ./web01data/: "./web01data/" includes invalid characters for a local volume name, only "[a-zA-Z0-9][a-zA-Z0-9_.-]" are allowed. If you intended to pass a host directory, use absolute path.
See 'docker run --help'.
$ docker run -dit --name web01 -v web01data:/usr/local/apache2/htdocs -p 9090:90 httpd:2.4
d746df07000135a44500cf4dceae1e3cb9a34a3c250afdb5b3de147878f0bee5
$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                          NAMES
d746df070001        httpd:2.4           "httpd-foreground"   5 seconds ago       Up 4 seconds        80/tcp, 0.0.0.0:9090->90/tcp   web01
9526da19310d        httpd:2.4           "httpd-foreground"   15 minutes ago      Up 15 minutes       0.0.0.0:8081->80/tcp           web02
$ curl localhost:9090
curl: (52) Empty reply from server
$ docker stop web01
web01
$ docker rm web01
web01

$ echo "I'm noticed [9090:90] is wronded. correct is [9090:80]."

$ docker run -dit --name web01 -v web01data:/usr/local/apache2/htdocs -p 8080:80 httpd:2.4
4be6535dcc944a85e4e2de49ea032b53f272edd346a82928538f6ef8a248bec0
$ curl localhost:8080
<html><body><h1>It works!</h1></body></html>
$ ll
total 96
drwxr-xr-x  12 kota.oue  staff   384  8 11 08:32 .
drwxr-xr-x  12 kota.oue  staff   384  8  9 19:14 ..
drwxr-xr-x  15 kota.oue  staff   480  8 11 08:36 .git
-rw-r--r--   1 kota.oue  staff   196  8  9 19:14 README.md
-rw-r--r--   1 kota.oue  staff    99  8  9 19:18 ch-2.md
-rw-r--r--   1 kota.oue  staff  4431  8  9 20:45 ch-3.md
-rw-r--r--   1 kota.oue  staff  9557  8  9 20:56 ch-4.md
-rw-r--r--   1 kota.oue  staff  5489  8 11 08:36 ch-5.md
-rw-r--r--   1 kota.oue  staff    86  8  9 19:31 index.html
-rw-r--r--   1 kota.oue  staff    87  8 11 08:26 index2.html
-rw-r--r--   1 kota.oue  staff    72  8  9 20:50 main.go
drwxr-xr-x   3 kota.oue  staff    96  8 11 08:33 web01data
$ docker stop web01
web01
$ docker rm web01
web01

$ docker run -dit --name web01 -v ./web01data:/usr/local/apache2/htdocs -p 8080:80 httpd:2.4
docker: Error response from daemon: create ./web01data: "./web01data" includes invalid characters for a local volume name, only "[a-zA-Z0-9][a-zA-Z0-9_.-]" are allowed. If you intended to pass a host directory, use absolute path.
See 'docker run --help'.
$ docker run -dit --name web01 -v "$PWD"/web01data:/usr/local/apache2/htdocs -p 8080:80 httpd:2.4
7db59e088a88b9ee8b5262a1968e0b5b7650550510dffb72b2993d068ca7198b
$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
7db59e088a88        httpd:2.4           "httpd-foreground"   7 seconds ago       Up 6 seconds        0.0.0.0:8080->80/tcp   web01
9526da19310d        httpd:2.4           "httpd-foreground"   26 minutes ago      Up 26 minutes       0.0.0.0:8081->80/tcp   web02
$ curl localhost:8080
<html>
<head>
<title>index.html</title>
</head>
<body>
I'm web01data/index.html
</body>
</html>

$ docker stop web01
web01
$ docker rm web01
web01
$ docker run -dit --name web01 -v "$PWD"/web01data:/usr/local/apache2/htdocs -p 8080:80 httpd:2.4
884c68abdfbc93476fb10b11309df1911d6007ff1da96beaa93e5de450442394
$ curl localhost:8080
<html>
<head>
<title>index.html</title>
</head>
<body>
I'm web01data/index.html
</body>
</html>
$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
884c68abdfbc        httpd:2.4           "httpd-foreground"   33 seconds ago      Up 32 seconds       0.0.0.0:8080->80/tcp   web01
9526da19310d        httpd:2.4           "httpd-foreground"   27 minutes ago      Up 27 minutes       0.0.0.0:8081->80/tcp   web02

$ docker_search_tags mysql | grep 5.7
"name": "5.7"
"name": "5.7.10"
"name": "5.7.11"
"name": "5.7.12"
"name": "5.7.13"
"name": "5.7.14"
"name": "5.7.15"
"name": "5.7.16"
"name": "5.7.17"
"name": "5.7.18"
"name": "5.7.19"
"name": "5.7.20"
"name": "5.7.21"
"name": "5.7.22"
"name": "5.7.23"
"name": "5.7.24"
"name": "5.7.25"
"name": "5.7.26"
"name": "5.7.27"
"name": "5.7.28"
"name": "5.7.29"
"name": "5.7.30"
"name": "5.7.31"
"name": "5.7.4"
"name": "5.7.4-m14"
"name": "5.7.5"
"name": "5.7.5-m15"
"name": "5.7.6"
"name": "5.7.6-m16"
"name": "5.7.7"
"name": "5.7.7-rc"
"name": "5.7.8"
"name": "5.7.8-rc"
"name": "5.7.9"

$ docker volume create mysqlvolume
mysqlvolume
$ docker volume ls
DRIVER              VOLUME NAME
local               mysqlvolume
$ docker run --name db01 -dit -v mysqlvolume:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=mypassword mysql:5.7
e7b2c287c734b1da0ef1653fbfb4f2c4388a3262d8a0d14a99d5e73bd305646f
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                 NAMES
e7b2c287c734        mysql:5.7           "docker-entrypoint.s…"   About a minute ago   Up About a minute   3306/tcp, 33060/tcp   db01
```