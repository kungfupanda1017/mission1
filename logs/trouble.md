```bash
$ docker run -d -p 8080:80 --name conflict-test my-web:1.0
76f04f0a091f4b4c391ede8de7886f4902a8b77489050984c251f2f05215b257
docker: Error response from daemon: failed to set up container networking: driver failed programming external connectivity on endpoint conflict-test (3620fd0c8571930469a80d2c79270fab780fc5a311ee868bebfb4a1c597d67c7): Bind for 0.0.0.0:8080 failed: port is already allocated

Run 'docker run --help' for more information
```

```bash
$ docker ps --format '{{.Names}} {{.Ports}}'
my-web-8081 0.0.0.0:8081->80/tcp, [::]:8081->80/tcp
my-web-8080 0.0.0.0:8080->80/tcp, [::]:8080->80/tcp
```

```bash
$ docker run -d -p 8083:80 --name conflict-test my-web:1.0
docker: Error response from daemon: Conflict. The container name "/conflict-test" is already in use by container "76f04f0a091f4b4c391ede8de7886f4902a8b77489050984c251f2f05215b257". You have to remove (or rename) that container to be able to reuse that name.

Run 'docker run --help' for more information
```

```bash
$ docker rm -f conflict-test
conflict-test
```

