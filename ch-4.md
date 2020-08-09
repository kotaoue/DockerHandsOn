```ShellSession
$ cd ~/ghq/github.com/kotaoue/DockerHandsOn/
$ docker pull httpd:2.4
2.4: Pulling from library/httpd
bf5952930446: Pull complete 
3d3fecf6569b: Pull complete 
b5fc3125d912: Pull complete 
679d69c01e90: Pull complete 
76291586768e: Pull complete 
Digest: sha256:3cbdff4bc16681541885ccf1524a532afa28d2a6578ab7c2d5154a7abc182379
Status: Downloaded newer image for httpd:2.4
docker.io/library/httpd:2.4
$ docker create --name my-apache-app -p 8080:80 -v "$PWD":/usr/local/apach2/htdocs/ httpd:2.4
3a23fd8e85e6851f63b7386aa703ed4356b6b4242530716b63fcc50008567c32
$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
3a23fd8e85e6        httpd:2.4           "httpd-foreground"   24 seconds ago      Up 5 seconds        0.0.0.0:8080->80/tcp   my-apache-app
$ curl localhost:8080
<html><body><h1>It works!</h1></body></html>
$ curl https://registry.hub.docker.com/v1/repositories/php/tags 2>&1 | grep -o "\"name\": \"8.0.0alpha[^}]*"
"name": "8.0.0alpha1"
"name": "8.0.0alpha1-alpine"
"name": "8.0.0alpha1-alpine3.12"
"name": "8.0.0alpha1-apache"
"name": "8.0.0alpha1-apache-buster"
"name": "8.0.0alpha1-buster"
"name": "8.0.0alpha1-cli"
"name": "8.0.0alpha1-cli-alpine"
"name": "8.0.0alpha1-cli-alpine3.12"
"name": "8.0.0alpha1-cli-buster"
"name": "8.0.0alpha1-fpm"
"name": "8.0.0alpha1-fpm-alpine"
"name": "8.0.0alpha1-fpm-alpine3.12"
"name": "8.0.0alpha1-fpm-buster"
"name": "8.0.0alpha1-zts"
"name": "8.0.0alpha1-zts-buster"
"name": "8.0.0alpha2"
"name": "8.0.0alpha2-alpine"
"name": "8.0.0alpha2-alpine3.12"
"name": "8.0.0alpha2-apache"
"name": "8.0.0alpha2-apache-buster"
"name": "8.0.0alpha2-buster"
"name": "8.0.0alpha2-cli"
"name": "8.0.0alpha2-cli-alpine"
"name": "8.0.0alpha2-cli-alpine3.12"
"name": "8.0.0alpha2-cli-buster"
"name": "8.0.0alpha2-fpm"
"name": "8.0.0alpha2-fpm-alpine"
"name": "8.0.0alpha2-fpm-alpine3.12"
"name": "8.0.0alpha2-fpm-buster"
"name": "8.0.0alpha2-zts"
"name": "8.0.0alpha2-zts-buster"
"name": "8.0.0alpha3"
"name": "8.0.0alpha3-alpine"
"name": "8.0.0alpha3-alpine3.12"
"name": "8.0.0alpha3-apache"
"name": "8.0.0alpha3-apache-buster"
"name": "8.0.0alpha3-buster"
"name": "8.0.0alpha3-cli"
"name": "8.0.0alpha3-cli-alpine"
"name": "8.0.0alpha3-cli-alpine3.12"
"name": "8.0.0alpha3-cli-buster"
"name": "8.0.0alpha3-fpm"
"name": "8.0.0alpha3-fpm-alpine"
"name": "8.0.0alpha3-fpm-alpine3.12"
"name": "8.0.0alpha3-fpm-buster"
"name": "8.0.0alpha3-zts"
"name": "8.0.0alpha3-zts-buster"
$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
3a23fd8e85e6        httpd:2.4           "httpd-foreground"   36 minutes ago      Up 2 minutes        0.0.0.0:8080->80/tcp   my-apache-app
$ docker kill my-apache-app
my-apache-app
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

$ docker run --name my-apache-app -p 8080:80 -v "$PWD":/usr/local/apache2/htdocs/ httpd:2.4
docker: Error response from daemon: Conflict. The container name "/my-apache-app" is already in use by container "3a23fd8e85e6851f63b7386aa703ed4356b6b4242530716b63fcc50008567c32". You have to remove (or rename) that container to be able to reuse that name.
See 'docker run --help'.
$ docker rm my-apache-app
my-apache-app
$ docker run --name my-apache-app -p 8080:80 -v "$PWD":/usr/local/apache2/htdocs/ httpd:2.4
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
[Sun Aug 09 11:29:39.606621 2020] [mpm_event:notice] [pid 1:tid 139823418066048] AH00489: Apache/2.4.46 (Unix) configured -- resuming normal operations
[Sun Aug 09 11:29:39.607797 2020] [core:notice] [pid 1:tid 139823418066048] AH00094: Command line: 'httpd -D FOREGROUND'
^C[Sun Aug 09 11:29:52.478245 2020] [mpm_event:notice] [pid 1:tid 139823418066048] AH00491: caught SIGTERM, shutting down
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS                                NAMES
07968eea4a12        httpd:2.4           "httpd-foreground"       40 seconds ago      Exited (0) 27 seconds ago                                        my-apache-app
$ docker rm my-apache-app
my-apache-app

$ docker run -it --name my-apache-app -p 8080:80 -v "$PWD":/usr/local/apache2/htdocs/ httpd:2.4
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
[Sun Aug 09 11:32:40.287585 2020] [mpm_event:notice] [pid 1:tid 140712158729344] AH00489: Apache/2.4.46 (Unix) configured -- resuming normal operations
[Sun Aug 09 11:32:40.287716 2020] [core:notice] [pid 1:tid 140712158729344] AH00094: Command line: 'httpd -D FOREGROUND'
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                     PORTS                                NAMES
e8f53fb13e16        httpd:2.4           "httpd-foreground"       34 seconds ago      Up 33 seconds              0.0.0.0:8080->80/tcp                 my-apache-app
$ docker attach my-apache-app
[Sun Aug 09 11:33:39.509713 2020] [mpm_event:notice] [pid 1:tid 140712158729344] AH00492: caught SIGWINCH, shutting down gracefully
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS                      PORTS                                NAMES
e8f53fb13e16        httpd:2.4           "httpd-foreground"       About a minute ago   Exited (0) 13 seconds ago                                        my-apache-app
$ docker rm my-apache-app
my-apache-app
```