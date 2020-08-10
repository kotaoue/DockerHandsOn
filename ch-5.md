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
```