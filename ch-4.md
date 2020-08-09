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
```