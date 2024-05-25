# My smart home
<img src="https://www.home-assistant.io/images/blog/2023-09-ha10/home-assistant-logo-new.png" alt="drawing" width="300"/>


## IP proxy
Use [Nginx proxy manager](https://github.com/VolokzhaninVadim/npm)
Get ip docker:
```bash
docker inspect \
  -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' docker_name_or_id
```
For fixing error [`400: Bad Request`](https://github.com/hassio-addons/addon-nginx-proxy-manager/issues/369) edit `./config_homeassistant/configuration.yaml`:
```bash
http:
  use_x_forwarded_for: true
  trusted_proxies:
    - 172.30.0.0/24 # You may also provide the subnet mask
```