# ZeroTier
### Pull and Run container
```
podman pull tailscale/tailscale:latest
podman run -d --name tailscale \
-v /var/lib:/var/lib \
-v /dev/net/tun:/dev/net/tun \
--network=host \
--cap-add=NET_ADMIN \
--cap-add=NET_RAW \
-e TS_EXTRA_ARGS="--accept-routes --exit-node=x.x.x.x" \
-e TS_AUTHKEY=tskey-auth-XXXXXX \
-e TS_SOCKS5_SERVER=:8383
-e TS_OUTBOUND_HTTP_PROXY_LISTEN=:8383
-e TS_HOSTNAME=YourHostname
tailscale/tailscale:latest
```

### Attach to container
```
podman exec -it tailscale bash
```

### Remove container
```
podman stop tailscale
podman rm tailscale
```

### Source
[https://hub.docker.com/r/tailscale/tailscale](https://hub.docker.com/r/tailscale/tailscale)  