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

$ docker container inspect --format="{{.NetworkSettings.IPAddress}}" web01
172.17.0.2
$ docker container inspect --format="{{.NetworkSettings}}" web01
{{ 00919c1d70b3ad2903aee949561f2203072197f1ab32752cc686a40fcf8c4e65 false  0 map[80/tcp:[{0.0.0.0 8080}]] /var/run/docker/netns/00919c1d70b3 [] []} {0a5962d24143e5b4e069b4e61fe7e1a2fa96b36ddb003180ee76fd7eae796557 172.17.0.1  0 172.17.0.2 16  02:42:ac:11:00:02} map[bridge:0xc0005a0000]}

$ docker container inspect --format='{{range $p, $conf :=.NetworkSettings.Ports}} {{$p}} -. {{(index $conf 0).HostPort}}{{end}}' web01 80/tcp -> 8080
Error: No such container: 80/tcp
Error: No such container: -
$ docker container inspect --format='{{range $p, $conf :=.NetworkSettings.Ports}} {{$p}} -> {{(index $conf 0).HostPort}}{{end}}' web01 80/tcp -> 8080
Error: No such container: 80/tcp
Error: No such container: -
$ docker inspect --format='{{range $p, $conf :=.NetworkSettings.Ports}} {{$p}} -> {{(index $conf 0).HostPort}}{{end}}' web01 80/tcp -> 8080
Error: No such object: 80/tcp
Error: No such object: -
$ docker inspect --format='{{range $p, $conf := .NetworkSettings.Ports}} {{$p}} -> {{(index $conf 0).HostPort}} {{end}}' web01
 80/tcp -> 8080

$ docker container inspect --format="{{.NetworkSettings.IPAddress}}" web01
172.17.0.2
$ docker container inspect --format="{{.NetworkSettings.IPAddress}}" web02
172.17.0.3

$ docker network inspect --format='{{range $host, $conf := .Containers}}{{$conf.Name}}->{{$conf.IPv4Address}}{{"\n"}}{{end}}' bridge
web01->172.17.0.2/16
web02->172.17.0.3/16

$ docker network inspect --format='{{range $host, $conf := .Containers}}{{$conf.Name}}->{{$conf.IPv4Address}}{{","}}{{end}}' bridge
web01->172.17.0.2/16,web02->172.17.0.3/16,
$ docker network inspect --format='{{range $host, $conf := .Containers}}{{$conf.Name}}->{{$conf.IPv4Address}}{{", "}}{{end}}' bridge
web01->172.17.0.2/16, web02->172.17.0.3/16, 
```