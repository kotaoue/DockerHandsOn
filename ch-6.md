```ShellSession
$ cd ~/ghq/github.com/kotaoue/DockerHandsOn/

$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
a1e8a0a71a42        bridge              bridge              local
d9704bca11b9        host                host                local
42eed01f7563        none                null                local

$ docker run -dit --name web01 -p 8080:80 httpd:2.4
0965915c2c9f3190eb68a6952bc7a8f287005fb250b2efb4e219cefb7a0bdf7f
$ docker run -dit --name web02 -p 8081:80 httpd:2.4
48ad01e21077df17f798e9f5d4cd9ba9ed26c5e8d7099f0fd2bf6b0eb7d9f9ed
$ docker exec -it web01 /bin/bash
root@0965915c2c9f:/usr/local/apache2# ifconfig
bash: ifconfig: command not found
root@0965915c2c9f:/usr/local/apache2# exit
exit
```