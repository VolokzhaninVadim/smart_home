# My smart home
![](./img/smart_home.png)

## IP proxy
Use [Nginx proxy manager](https://github.com/VolokzhaninVadim/npm)

Get ip docker:
```bash
docker inspect \
  -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' docker_name_or_id
```
For fixing error [`400: Bad Request`](https://github.com/hassio-addons/addon-nginx-proxy-manager/issues/369) edit `./config_homeassistant/configuration.yaml`:
```bash
# DNS proxy
http:
  use_x_forwarded_for: true
  trusted_proxies:
    - 172.30.0.0/24 # You may also provide the subnet mask
```

## Database
Execute:
1. `docker exec -it homeassistant-postgres psql -U postgresadmin`
1. `CREATE USER homeassistant WITH PASSWORD 'yourHomeAsssistantPassword';`
1. `CREATE DATABASE homeassistant WITH OWNER homeassistant ENCODING 'utf8';`

Edit `configuration.yaml`:
```yaml
# Database
recorder:
  db_url: !secret psql_connector_string
  db_retry_wait: 10 # Wait 10 seconds before retrying
```
```bash
psql_connector_string: "postgresql://DATABSE_USERNAME:DATABASE_PASSWORD@DNSNAME_OR_IP_OF_POSTGRES_SERVER/DATABASE_NAME"
```

## [HACS](https://hacs.xyz/docs/setup/download/)
```bash
docker exec -it homeassistant bash
cd /
wget -O - https://get.hacs.xyz | bash -
```

## Smartphone
1. For smartphone use [Home Assistant](https://f-droid.org/packages/io.homeassistant.companion.android.minimal/).
1. For 2FA use [FreeOTP+](https://f-droid.org/ru/packages/org.liberty.android.freeotpplus/)