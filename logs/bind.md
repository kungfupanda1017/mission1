```bash
$ docker run -d --name bind-test -p 8082:80 -v ~/mission1/site:/usr/share/nginx/html:ro nginx:alpine
af8393f83db14be5ef9b2d7bb2807fd62112ee6172d07a98f930aa50cd7d9500
```

```bash
$ curl -s http://localhost:8082
<h1>BEFORE</h1>
```

```bash
$ curl -s http://localhost:8082
<h1>AFTER</h1>
```

```bash
$ docker rm -f bind-test
bind-test
```

