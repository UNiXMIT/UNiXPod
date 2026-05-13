# rsyslog
### Pull and Run container
```
podman pull rsyslog/rsyslog-collector:latest
podman run -d --name rsyslog \
-p 5514:514/tcp \
-p 5514:514/udp \
# TLS
# -p 6514:6514/tcp \
-v /home/support/rsyslog:/var/log
rsyslog/rsyslog-collector:latest
```

### Attach to container
```
podman exec -it rsyslog bash
```

### Healthcheck
```
--health-cmd "logger -n 127.0.0.1 -P 514 healthcheck 'rsyslog-healthcheck' && exit 0 || exit 1" \
--health-interval 1m \
--health-timeout 10s \
--health-retries 5 \
--health-start-period 1m \
```

### Remove your container
```
podman stop rsyslog
podman rm rsyslog
```

### Source
https://hub.docker.com/r/rsyslog/rsyslog-collector