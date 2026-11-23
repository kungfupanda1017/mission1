```bash
$ docker pull nginx:alpine
alpine: Pulling from library/nginx
c4f3d97811f6: Pulling fs layer
881fc932939e: Pulling fs layer
77a3bfea78f5: Pulling fs layer
61d8f4c85a74: Pulling fs layer
04c3905a997c: Pulling fs layer
1dc588c89da1: Pulling fs layer
7cb374baf968: Pulling fs layer
4c8c172c6586: Pulling fs layer
881fc932939e: Download complete
1dc588c89da1: Download complete
4c8c172c6586: Download complete
04c3905a997c: Download complete
7cb374baf968: Download complete
77a3bfea78f5: Download complete
61d8f4c85a74: Download complete
c4f3d97811f6: Download complete
881fc932939e: Pull complete
04c3905a997c: Pull complete
77a3bfea78f5: Pull complete
1dc588c89da1: Pull complete
4c8c172c6586: Pull complete
7cb374baf968: Pull complete
61d8f4c85a74: Pull complete
79979b969278: Download complete
33247e384332: Download complete
c4f3d97811f6: Pull complete
Digest: sha256:fb4658584bd9a916ffb6f6e365f97c25cfdb2923801f551ea08356e695f14ff7
Status: Downloaded newer image for nginx:alpine
docker.io/library/nginx:alpine
```

```bash
$ docker images
IMAGE                ID             DISK USAGE   CONTENT SIZE   EXTRA
hello-world:latest   c567b231f656       25.9kB         9.49kB   U    
nginx:alpine         fb4658584bd9       94.5MB         27.2MB        
nginx:latest         5ab5b0b01097        243MB         66.8MB        
```

```bash
$ docker run -d --name ops-test nginx:alpine
40afcd320391226e66189021a96cefb7fa9fdc6427c8f02e21cc860de673c979
```

```bash
$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS     NAMES
40afcd320391   nginx:alpine   "/docker-entrypoint.…"   4 seconds ago   Up 4 seconds   80/tcp    ops-test
```

```bash
$ docker logs ops-test
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2026/11/23 04:52:57 [notice] 1#1: using the "epoll" event method
2026/11/23 04:52:57 [notice] 1#1: nginx/1.31.9
2026/11/23 04:52:57 [notice] 1#1: built by gcc 15.2.0 (Alpine 15.2.0) 
2026/11/23 04:52:57 [notice] 1#1: OS: Linux 6.18.58.1-microsoft-standard-WSL2
2026/11/23 04:52:57 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1024:1048576
2026/11/23 04:52:57 [notice] 1#1: start worker processes
2026/11/23 04:52:57 [notice] 1#1: start worker process 30
2026/11/23 04:52:57 [notice] 1#1: start worker process 31
2026/11/23 04:52:57 [notice] 1#1: start worker process 32
2026/11/23 04:52:57 [notice] 1#1: start worker process 33
2026/11/23 04:52:57 [notice] 1#1: start worker process 34
2026/11/23 04:52:57 [notice] 1#1: start worker process 35
2026/11/23 04:52:57 [notice] 1#1: start worker process 36
2026/11/23 04:52:57 [notice] 1#1: start worker process 37
2026/11/23 04:52:57 [notice] 1#1: start worker process 38
2026/11/23 04:52:57 [notice] 1#1: start worker process 39
2026/11/23 04:52:57 [notice] 1#1: start worker process 40
2026/11/23 04:52:57 [notice] 1#1: start worker process 41
2026/11/23 04:52:57 [notice] 1#1: start worker process 42
2026/11/23 04:52:57 [notice] 1#1: start worker process 43
2026/11/23 04:52:57 [notice] 1#1: start worker process 44
2026/11/23 04:52:57 [notice] 1#1: start worker process 45
2026/11/23 04:52:57 [notice] 1#1: start worker process 46
2026/11/23 04:52:57 [notice] 1#1: start worker process 47
2026/11/23 04:52:57 [notice] 1#1: start worker process 48
2026/11/23 04:52:57 [notice] 1#1: start worker process 49
2026/11/23 04:52:57 [notice] 1#1: start worker process 50
2026/11/23 04:52:57 [notice] 1#1: start worker process 51
2026/11/23 04:52:57 [notice] 1#1: start worker process 52
2026/11/23 04:52:57 [notice] 1#1: start worker process 53
```

```bash
$ docker stats --no-stream
CONTAINER ID   NAME       CPU %     MEM USAGE / LIMIT     MEM %     NET I/O         BLOCK I/O     PIDS
40afcd320391   ops-test   0.00%     21.26MiB / 15.25GiB   0.14%     1.18kB / 126B   0B / 8.19kB   25
```

```bash
$ docker stop ops-test
ops-test
```

```bash
$ docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                     PORTS     NAMES
40afcd320391   nginx:alpine   "/docker-entrypoint.…"   23 seconds ago   Exited (0) 4 seconds ago             ops-test
4165541ac9aa   hello-world    "/hello"                 2 weeks ago      Exited (0) 2 weeks ago               intelligent_elion
```

```bash
$ docker start ops-test
ops-test
```

```bash
$ docker rm -f ops-test
ops-test
```

