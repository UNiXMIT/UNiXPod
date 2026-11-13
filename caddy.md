# Caddy
### Pull and Run container
```
podman pull caddy
podman run -d -v /home/support/caddy/conf:/etc/caddy \
              -v /home/support/caddy/data:/data \
              -v /home/support/caddy/config:/config \
              -p 80:80 -p 443:443 -p 443:443/udp \
              --cap-add NET_ADMIN \
              --name caddy caddy
```

### Attach to container
```
podman exec -it caddy bash
``` 

### Remove your container
```
podman stop caddy
podman rm caddy
```

### Source
https://hub.docker.com/_/caddy