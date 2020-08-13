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

$ docker run --name wordpress-db -dit --mount type=volume,src=wordpress_db_volume,dst=/var/lib/mysql -e MYSQL_ROOT_PASSWORD=rootpass -e MYSQL_DATABASE=wpdb -e MYSQL_USER=wpuser -e MYSQL_PASSWORD=wppass --net wordpressnet mysql:5.7
1894dfe557f2679a04b79991c7fc347aad57af82b8cfd40e5c56ebc21617ad78
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
1894dfe557f2        mysql:5.7           "docker-entrypoint.s…"   5 seconds ago       Up 4 seconds        3306/tcp, 33060/tcp   wordpress-db
```