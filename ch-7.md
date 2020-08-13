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
```