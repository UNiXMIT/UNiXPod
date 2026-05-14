# SOCKS5 Proxy
### Pull and Run container
```
podman pull serjs/go-socks5-proxy:latest
podman run -d --name socks \
-p 1080:1080 \
-e REQUIRE_AUTH=true \
-e PROXY_USER=support \
-e PROXY_PASSWORD=strongPassword#123 \
serjs/go-socks5-proxy:latest
```

### Test SOCKS Proxy
```
curl --proxy socks5h://127.0.0.1:1080 -U support:strongPassword#123 
```

### Attach to container
```
podman exec -it socks bash
```

### Remove container
```
podman stop socks
podman rm socks
```

### Source
[https://github.com/serjs/socks5-server](https://github.com/serjs/socks5-server)  