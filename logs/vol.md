```bash
$ docker volume create mydata
mydata
```

```bash
$ docker run -d --name vol-test -v mydata:/data ubuntu sleep infinity
b1a6918aa561cdf51ddfaf1dd3b926de0b1d3d1a55738477d4b2b9231c8767ce
```

```bash
$ docker exec vol-test bash -c 'echo hi > /data/hello.txt && cat /data/hello.txt'
hi
```

```bash
$ docker rm -f vol-test
vol-test
```

```bash
$ docker ps -a --filter name=vol-test
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

```bash
$ docker volume ls --filter name=mydata
DRIVER    VOLUME NAME
local     mydata
```

```bash
$ docker run -d --name vol-test2 -v mydata:/data ubuntu sleep infinity
296462b971e1f3e77be8470f4062e67ffbabd31fcb2621f7bd63bc56f75a3869
```

```bash
$ docker exec vol-test2 cat /data/hello.txt
hi
```

```bash
$ docker volume inspect mydata
[
    {
        "CreatedAt": "2026-11-23T14:25:55+09:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/mydata/_data",
        "Name": "mydata",
        "Options": null,
        "Scope": "local"
    }
]
```

```bash
$ docker rm -f vol-test2
vol-test2
```

