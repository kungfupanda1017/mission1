```bash
$ docker build -t my-web:1.0 .
#0 building with "default" instance using docker driver

#1 [internal] load build definition from Dockerfile
#1 transferring dockerfile: 187B done
#1 DONE 0.0s

#2 [internal] load metadata for docker.io/library/nginx:alpine
#2 DONE 0.0s

#3 [internal] load .dockerignore
#3 transferring context: 2B done
#3 DONE 0.0s

#4 [internal] load build context
#4 transferring context: 61B done
#4 DONE 0.0s

#5 [1/2] FROM docker.io/library/nginx:alpine@sha256:fb4658584bd9a916ffb6f6e365f97c25cfdb2923801f551ea08356e695f14ff7
#5 resolve docker.io/library/nginx:alpine@sha256:fb4658584bd9a916ffb6f6e365f97c25cfdb2923801f551ea08356e695f14ff7 0.0s done
#5 DONE 0.2s

#5 [1/2] FROM docker.io/library/nginx:alpine@sha256:fb4658584bd9a916ffb6f6e365f97c25cfdb2923801f551ea08356e695f14ff7
#5 extracting sha256:881fc932939efef04ca120ad44bbd2c0917851eb247aa4995428afb1e80ede17 0.1s done
#5 extracting sha256:77a3bfea78f562fc46a238affde2e413f44ebe98eb6accd78acc9aade0711eed 0.1s done
#5 DONE 0.3s

#5 [1/2] FROM docker.io/library/nginx:alpine@sha256:fb4658584bd9a916ffb6f6e365f97c25cfdb2923801f551ea08356e695f14ff7
#5 extracting sha256:04c3905a997c5ada93c8e4ad6c8d593e04c5ad4efa87a648a72f34138ea47117 0.0s done
#5 extracting sha256:7cb374baf96870045ef10fb2275d30d893e2010d5fb12d2e8f949babcb3de6bf 0.0s done
#5 extracting sha256:4c8c172c658661b7927fad4ab766c7e6c597d83400a3ed3f2e484c5940b4c56a 0.0s done
#5 extracting sha256:1dc588c89da10830dde2a359d1b421e384caaae52458be045dcf6770ae7d624a 0.0s done
#5 extracting sha256:61d8f4c85a745813b78f7b3ea04d0268fd196753e0964ac6cd3f55fe161c865b 0.0s done
#5 extracting sha256:c4f3d97811f679e18a790555496d98de98efbd4a61f8741c1aeedd86317c5f6c
#5 extracting sha256:c4f3d97811f679e18a790555496d98de98efbd4a61f8741c1aeedd86317c5f6c 0.2s done
#5 DONE 0.6s

#6 [2/2] COPY index.html /usr/share/nginx/html/index.html
#6 DONE 0.0s

#7 exporting to image
#7 exporting layers 0.1s done
#7 exporting manifest sha256:3f2d89cb7cfb7fb00b6a53a08901d46eabca24d403970c1a5b1959b83618d288 0.0s done
#7 exporting config sha256:5fe1439dff4b3171ec56635fb02a61d639c27173bc3205faaca18ad1411ca8f3 0.0s done
#7 exporting attestation manifest sha256:b79f518466494b73e93ce437b223c978059f2c4742896bf69131f85e554b9ecc 0.0s done
#7 exporting manifest list sha256:1ae8f374c14f51639d34d3f8c01e9bfb3fa3043b990d82fcd585ef482e0f53c3 0.0s done
#7 naming to docker.io/library/my-web:1.0 done
#7 unpacking to docker.io/library/my-web:1.0 0.0s done
#7 DONE 0.2s
```

```bash
$ docker run -d -p 8080:80 --name my-web-8080 my-web:1.0
427da6c600d9dbfb3204d87dda48cb9e737f0de64efef3206a61d33c06acfa32
```

```bash
$ docker run -d -p 8081:80 --name my-web-8081 my-web:1.0
b4d946cb284706ff04006d21b7165fbadb0e8f19f55bf6ca950a004aa7468d02
```

```bash
$ docker ps
CONTAINER ID   IMAGE        COMMAND                  CREATED          STATUS          PORTS                                     NAMES
b4d946cb2847   my-web:1.0   "/docker-entrypoint.…"   7 seconds ago    Up 6 seconds    0.0.0.0:8081->80/tcp, [::]:8081->80/tcp   my-web-8081
427da6c600d9   my-web:1.0   "/docker-entrypoint.…"   12 seconds ago   Up 11 seconds   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   my-web-8080
```

```bash
$ curl -s http://localhost:8080
<h1>Hello, Docker!</h1>
```

```bash
$ curl -s http://localhost:8081
<h1>Hello, Docker!</h1>
```

```bash
$ docker exec my-web-8080 printenv APP_ENV
dev
```

