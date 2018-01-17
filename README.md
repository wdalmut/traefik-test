# Traefik

## Install

```sh
docker-compose up -d
```

## API

### Override a service

First of all start a local service

```sh
echo "EXTERNAL" > index.php
php -S 0:8082 -t .
```

Then override with priority a running service

```sh
curl -XPUT http://localhost:8080/api/providers/web -d @create.json
```

The go to page: `http://test.127.0.0.1.xip.io/`

### Drop services

```sh
curl -XPUT http://localhost:8080/api/providers/web -d @delete.json
```

