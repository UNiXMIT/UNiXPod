# Shadowsocks

### Pull and Run container
```
podman pull shadowsocks/shadowsocks-libev:latest
podman run -d --name shadowsocks -e PASSWORD=strongPassword123 -e TZ=UTC -p 8388:8388 -p 8388:8388/udp shadowsocks/shadowsocks-libev:latest
```

### Attach to container
```
podman exec -it shadowsocks bash
```

### Remove your container
```
podman stop shadowsocks
podman rm shadowsocks
```

### Source
https://github.com/shadowsocks/shadowsocks-libev/blob/master/docker/alpine/README.md