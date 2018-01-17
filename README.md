# Traefik

## Install

```sh
docker-compose up -d
```

## API

### Override a service

Get your IP address

```
MYIP=$(ip addr show | grep -E '^\s*inet' | grep -m1 global | awk '{ print $2 }' | sed 's|/.*||')
```

Start a local service

```sh
echo "EXTERNAL" > index.php
php -S 0:8082 -t .
```

Update the JSON configuration

```sh
json -I -f create.json -e "this.backends[\"backend-test\"].servers.corley.url=\"http://$MYIP:8082/\""
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

