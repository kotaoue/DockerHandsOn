```ShellSession
$ cd ~/ghq/github.com/kotaoue/DockerHandsOn/
$ docker run -dit --name my-apache-app -p 8080:80 -v "$PWD":/usr/local/apache2/htdocs/ httpd:2.4
Unable to find image 'httpd:2.4' locally
2.4: Pulling from library/httpd
bf5952930446: Pull complete 
3d3fecf6569b: Pull complete 
b5fc3125d912: Pull complete 
679d69c01e90: Pull complete 
76291586768e: Pull complete 
Digest: sha256:3cbdff4bc16681541885ccf1524a532afa28d2a6578ab7c2d5154a7abc182379
Status: Downloaded newer image for httpd:2.4
6dc63bb2870d2e2f4cab5139ea82f4bf6fa2da7ee42418e73276bff1ab93d295
$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
6dc63bb2870d        httpd:2.4           "httpd-foreground"   38 seconds ago      Up 37 seconds       0.0.0.0:8080->80/tcp   my-apache-app
$ docker logs
"docker logs" requires exactly 1 argument.
See 'docker logs --help'.

Usage:  docker logs [OPTIONS] CONTAINER

Fetch the logs of a container
```