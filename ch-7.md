```ShellSession
$ cd ~/ghq/github.com/kotaoue/DockerHandsOn/

$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
a1e8a0a71a42        bridge              bridge              local
d9704bca11b9        host                host                local
42eed01f7563        none                null                local
31584fb54394        wordpressnet        bridge              local

$ docker volume prune
WARNING! This will remove all local volumes not used by at least one container.
Are you sure you want to continue? [y/N] y
Deleted Volumes:
mysqlvolume

Total reclaimed space: 413.9MB
$ docker volume ls
DRIVER              VOLUME NAME
$ docker volume create wordpress_db_volume
wordpress_db_volume
$ docker volume ls
DRIVER              VOLUME NAME
local               wordpress_db_volume

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

$ docker run --name wordpress-db -dit --mount type=volume,src=wordpress_db_volume,dst=/var/lib/mysql -e MYSQL_ROOT_PASSWORD=rootpass -e MYSQL_DATABASE=wpdb -e MYSQL_USER=wpuser -e MYSQL_PASSWORD=wppass --net wordpressnet mysql:5.7
1894dfe557f2679a04b79991c7fc347aad57af82b8cfd40e5c56ebc21617ad78
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
1894dfe557f2        mysql:5.7           "docker-entrypoint.s…"   5 seconds ago       Up 4 seconds        3306/tcp, 33060/tcp   wordpress-db 

$ docker_search_tags wordpress | wc -l
    1090
$ docker_search_tags wordpress | head
"name": "latest"
"name": "3"
"name": "3.9"
"name": "3.9.1"
"name": "3.9.2"
"name": "4"
"name": "4-apache"
"name": "4-fpm"
"name": "4-fpm-alpine"
"name": "4-php5.6"
```