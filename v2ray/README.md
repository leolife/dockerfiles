# Usage

## docker
```sh
docker pull idul/v2ray
docker run -d \
    -v your/v2ray/config.json:/app/config.json \
    -v your/v2ray/log/:/var/log/v2ray/ \
    -p 8000:8000 \
    idul/v2ray
```

## docker-compose
```yaml

version: "3"

services:
  v2ray:
    restart: always
    image: idul/v2ray
    ports:
     - 8000:8000
    volumes:
     - your/v2ray/config.json:/app/config.json
     - your/v2ray/log:/var/log/v2ray

```