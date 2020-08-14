```ShellSession
$ cd ~/ghq/github.com/kotaoue/DockerHandsOn/

$ docker image rm mysql:5.7
Untagged: mysql:5.7
Untagged: mysql@sha256:32f9d9a069f7a735e28fd44ea944d53c61f990ba71460c5c183e610854ca4854
Deleted: sha256:9cfcce23593a93135ca6dbf3ed544d1db9324d4c40b5c0d56958165bfaa2d46a
Deleted: sha256:98de3e212919056def8c639045293658f6e6022794807d4b0126945ddc8324be
Deleted: sha256:17e8b88858e400f8c5e10e7cb3fbab9477f6d8aacba03b8167d34a91dbe4d8c1
Deleted: sha256:c04c087c2af9abd64ba32fe89d65e6d83da514758923de5da154541cc01a3a1e
Deleted: sha256:ab8bf065b402b99aec4f12c648535ef1b8dc954b4e1773bdffa10ae2027d3e00
Deleted: sha256:09687cd9cdf4c704fde969fdba370c2d848bc614689712bef1a31d0d581f2007
Deleted: sha256:b704a4a65bf536f82e5d8b86e633d19185e26313de8380162e778feb2852011a
Deleted: sha256:c37206160543786228aa0cce738e85343173851faa44bb4dc07dc9b7dc4ff1c1
Deleted: sha256:12912c9ec523f648130e663d9d4f0a47c1841a0064d4152bcf7b2a97f96326eb
Deleted: sha256:57d29ad88aa49f0f439592755722e70710501b366e2be6125c95accc43464844
Deleted: sha256:b17c024283d0302615c6f0c825137da9db607d49a83d2215a79733afbbaeb7c3
Deleted: sha256:13cb14c2acd34e45446a50af25cb05095a17624678dbafbcc9e26086547c1d74
$ docker pull mysql:5.7
5.7: Pulling from library/mysql
bf5952930446: Already exists 
8254623a9871: Pull complete 
938e3e06dac4: Pull complete 
ea28ebf28884: Pull complete 
f3cef38785c2: Pull complete 
894f9792565a: Pull complete 
1d8a57523420: Pull complete 
5f09bf1d31c1: Pull complete 
1b6ff254abe7: Pull complete 
74310a0bf42d: Pull complete 
d398726627fd: Pull complete 
Digest: sha256:da58f943b94721d46e87d5de208dc07302a8b13e638cd1d24285d222376d6d84
Status: Downloaded newer image for mysql:5.7
docker.io/library/mysql:5.7
$ docker history ysql:5/7
Error response from daemon: No such image: ysql:5/7:latest
$ docker history mysql:5.7
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
718a6da099d8        9 days ago          /bin/sh -c #(nop)  CMD ["mysqld"]               0B                  
<missing>           9 days ago          /bin/sh -c #(nop)  EXPOSE 3306 33060            0B                  
<missing>           9 days ago          /bin/sh -c #(nop)  ENTRYPOINT ["docker-entry…   0B                  
<missing>           9 days ago          /bin/sh -c ln -s usr/local/bin/docker-entryp…   34B                 
<missing>           9 days ago          /bin/sh -c #(nop) COPY file:7cbb26bbdb8e71b3…   13.2kB              
<missing>           9 days ago          /bin/sh -c #(nop)  VOLUME [/var/lib/mysql]      0B                  
<missing>           9 days ago          /bin/sh -c {   echo mysql-community-server m…   313MB               
<missing>           9 days ago          /bin/sh -c echo "deb http://repo.mysql.com/a…   55B                 
<missing>           9 days ago          /bin/sh -c #(nop)  ENV MYSQL_VERSION=5.7.31-…   0B                  
<missing>           9 days ago          /bin/sh -c #(nop)  ENV MYSQL_MAJOR=5.7          0B                  
<missing>           9 days ago          /bin/sh -c set -ex;  key='A4A9406876FCBD3C45…   2.61kB              
<missing>           9 days ago          /bin/sh -c apt-get update && apt-get install…   52.2MB              
<missing>           9 days ago          /bin/sh -c mkdir /docker-entrypoint-initdb.d    0B                  
<missing>           9 days ago          /bin/sh -c set -eux;  savedAptMark="$(apt-ma…   4.17MB              
<missing>           9 days ago          /bin/sh -c #(nop)  ENV GOSU_VERSION=1.12        0B                  
<missing>           9 days ago          /bin/sh -c apt-get update && apt-get install…   9.34MB              
<missing>           9 days ago          /bin/sh -c groupadd -r mysql && useradd -r -…   329kB               
<missing>           9 days ago          /bin/sh -c #(nop)  CMD ["bash"]                 0B                  
<missing>           9 days ago          /bin/sh -c #(nop) ADD file:3af3091e7d2bb40bc…   69.2MB  

$ docker run -dit --name webcontet -p 8080:80 httpd:2.4
652adaf9d269afac7ddfb45f8e1ffce27255d0a25edbb9520b38b29a14d5da6b
$ docker cp index.html webcontet:/usr/local/apache2/htdocs
$ curl http://localhost:8080
<html>
<head>
<title>index.html</title>
</head>
<body>
I'm index.html
</body>
</html>

$ docker commit webcontet mycustomed_httpd
sha256:1f517ea946fc90c29e7117a5a0c1061a168845b4778f70dbee47cb8c136ec7b2
$ docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
mycustomed_httpd    latest              1f517ea946fc        7 seconds ago       166MB

$ docker image history mycustomed_httpd
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
1f517ea946fc        44 seconds ago      httpd-foreground                                88B                 
a6ea92c35c43        8 days ago          /bin/sh -c #(nop)  CMD ["httpd-foreground"]     0B                  
<missing>           8 days ago          /bin/sh -c #(nop)  EXPOSE 80                    0B                  
<missing>           8 days ago          /bin/sh -c #(nop) COPY file:c432ff61c4993ecd…   138B                
<missing>           8 days ago          /bin/sh -c #(nop)  STOPSIGNAL SIGWINCH          0B                  
<missing>           8 days ago          /bin/sh -c set -eux;   savedAptMark="$(apt-m…   61MB                
<missing>           8 days ago          /bin/sh -c #(nop)  ENV HTTPD_PATCHES=           0B                  
<missing>           8 days ago          /bin/sh -c #(nop)  ENV HTTPD_SHA256=740eddf6…   0B                  
<missing>           8 days ago          /bin/sh -c #(nop)  ENV HTTPD_VERSION=2.4.46     0B                  
<missing>           9 days ago          /bin/sh -c set -eux;  apt-get update;  apt-g…   35.4MB              
<missing>           9 days ago          /bin/sh -c #(nop) WORKDIR /usr/local/apache2    0B                  
<missing>           9 days ago          /bin/sh -c mkdir -p "$HTTPD_PREFIX"  && chow…   0B                  
<missing>           9 days ago          /bin/sh -c #(nop)  ENV PATH=/usr/local/apach…   0B                  
<missing>           9 days ago          /bin/sh -c #(nop)  ENV HTTPD_PREFIX=/usr/loc…   0B                  
<missing>           9 days ago          /bin/sh -c #(nop)  CMD ["bash"]                 0B                  
<missing>           9 days ago          /bin/sh -c #(nop) ADD file:3af3091e7d2bb40bc…   69.2MB   

$ docker run -dit --name webcontent_new -p 8081:80 mycustomed_httpd
7a97f16dde8660129b7d66e88762299195be9d7a9602e1c890fc36ea7b054bee
$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
7a97f16dde86        mycustomed_httpd    "httpd-foreground"   2 seconds ago       Up 2 seconds        0.0.0.0:8081->80/tcp   webcontent_new
652adaf9d269        httpd:2.4           "httpd-foreground"   3 minutes ago       Up 3 minutes        0.0.0.0:8080->80/tcp   webcontet
$ docker exec -it webcontent_new /bin/bash
root@7a97f16dde86:/usr/local/apache2# cd /usr/local/apache2/htdocs/
root@7a97f16dde86:/usr/local/apache2/htdocs# ls -la
total 16
drwxr-xr-x 1 root     root     4096 Aug 14 13:36 .
drwxr-xr-x 1 www-data www-data 4096 Aug  5 23:21 ..
-rw-r--r-- 1      502 dialout    86 Aug  9 10:31 index.html
root@7a97f16dde86:/usr/local/apache2/htdocs# cat index.html 
<html>
<head>
<title>index.html</title>
</head>
<body>
I'm index.html
</body>
</html>
root@7a97f16dde86:/usr/local/apache2/htdocs# exit
exit
$ curl http://localhost:8081
<html>
<head>
<title>index.html</title>
</head>
<body>
I'm index.html
</body>
</html>

$ docker stop webcontet webcontet
webcontet
webcontet
$ docker rm webcontet webcontet
webcontet
Error response from daemon: removal of container webcontet is already in progress
$ docker stop webcontet webcontet_new
Error response from daemon: No such container: webcontet
Error response from daemon: No such container: webcontet_new
$ docker stop webcontet webcontent_new
webcontent_new
Error response from daemon: No such container: webcontet
$ docker rm webcontet webcontent_new
webcontent_new
Error: No such container: webcontet
$ docker image rm mycustomed_httpd
Untagged: mycustomed_httpd:latest
Deleted: sha256:1f517ea946fc90c29e7117a5a0c1061a168845b4778f70dbee47cb8c136ec7b2
Deleted: sha256:ad8102bd7f27aba602831422007607c0dd84a035dc987534c0d0fa2de865568d

$ mkdir customed_httpd
$ cd customed_httpd/
$ ll
total 0
drwxr-xr-x   2 kota.oue  staff   64  8 14 22:43 .
drwxr-xr-x  18 kota.oue  staff  576  8 14 22:43 ..
$ cp ../index.html index.html
$ ll
total 8
drwxr-xr-x   3 kota.oue  staff   96  8 14 22:44 .
drwxr-xr-x  18 kota.oue  staff  576  8 14 22:43 ..
-rw-r--r--   1 kota.oue  staff   86  8 14 22:44 index.html

$ touch Dockerfile
$ docker build -t myimage01 .
Sending build context to Docker daemon  3.072kB
Step 1/2 : FROM httpd
latest: Pulling from library/httpd
Digest: sha256:3cbdff4bc16681541885ccf1524a532afa28d2a6578ab7c2d5154a7abc182379
Status: Downloaded newer image for httpd:latest
 ---> a6ea92c35c43
Step 2/2 : COPY index.html /usr/local/apache2/htdocs
 ---> be172496cc27
Successfully built be172496cc27
Successfully tagged myimage01:latest
$ docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
myimage01           latest              be172496cc27        5 seconds ago       166MB
$ docker history myimage01
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
be172496cc27        14 seconds ago      /bin/sh -c #(nop) COPY file:eb5f451621c7d777…   86B                 
a6ea92c35c43        8 days ago          /bin/sh -c #(nop)  CMD ["httpd-foreground"]     0B                  
<missing>           8 days ago          /bin/sh -c #(nop)  EXPOSE 80                    0B                  
<missing>           8 days ago          /bin/sh -c #(nop) COPY file:c432ff61c4993ecd…   138B                
<missing>           8 days ago          /bin/sh -c #(nop)  STOPSIGNAL SIGWINCH          0B                  
<missing>           8 days ago          /bin/sh -c set -eux;   savedAptMark="$(apt-m…   61MB                
<missing>           8 days ago          /bin/sh -c #(nop)  ENV HTTPD_PATCHES=           0B                  
<missing>           8 days ago          /bin/sh -c #(nop)  ENV HTTPD_SHA256=740eddf6…   0B                  
<missing>           8 days ago          /bin/sh -c #(nop)  ENV HTTPD_VERSION=2.4.46     0B                  
<missing>           9 days ago          /bin/sh -c set -eux;  apt-get update;  apt-g…   35.4MB              
<missing>           9 days ago          /bin/sh -c #(nop) WORKDIR /usr/local/apache2    0B                  
<missing>           9 days ago          /bin/sh -c mkdir -p "$HTTPD_PREFIX"  && chow…   0B                  
<missing>           9 days ago          /bin/sh -c #(nop)  ENV PATH=/usr/local/apach…   0B                  
<missing>           9 days ago          /bin/sh -c #(nop)  ENV HTTPD_PREFIX=/usr/loc…   0B                  
<missing>           9 days ago          /bin/sh -c #(nop)  CMD ["bash"]                 0B                  
<missing>           9 days ago          /bin/sh -c #(nop) ADD file:3af3091e7d2bb40bc…   69.2MB   

$ docker run -dit --name webcontent_docker -p 8080:80 myimage01
60a3fdc8db0f35ca96e31577f9e9ca24cc77dee8f321a13bd028bad890636900
$ curl http://localhost:8080
<html>
<head>
<title>index.html</title>
</head>
<body>
I'm index.html
</body>
</html>

$ docker stop webcontet_docker
Error response from daemon: No such container: webcontet_docker
$ docker stop webcontent_docker
webcontent_docker
$ docker rm webcontent_docker
webcontent_docker
$ docker image rm myimage01
Untagged: myimage01:latest
Deleted: sha256:be172496cc274cbcf779d365adbc15fefc3920481605ab1bddeb4d8446c30dba
Deleted: sha256:6e61caaaae8c80d62bbc688309a173b14609b118777340c00d1f24ecb570c16c

$ curl -s https://github.com/docker-library/httpd/tree/master/2.4 | head





<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
  <link rel="dns-prefetch" href="https://github.githubassets.com">

$ cd ..
$ mkdir phpimage
$ cd phpimage/
```