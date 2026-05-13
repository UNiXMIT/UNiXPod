# Redis
### Pull and Run container
```
podman pull lscr.io/linuxserver/syslog-ng:latest
podman run -d --name syslogng \
-e PUID=1000 -e PGID=1000 \
-e TZ=Europe/London \
-p 6601:6601/tcp \
-p 5514:5514/udp \
-p 6514:6514/tcp \
-v /home/support/syslogng:/var/log
--health-cmd "syslog-ng-ctl --control=/config/syslog-ng.ctl healthcheck" \
--health-interval 1m \
--health-timeout 10s \
--health-retries 5 \
--health-start-period 1m \
lscr.io/linuxserver/syslog-ng:latest
```

### Ports
| Port | Service |
|------|---------|
| 5514 | Syslog UDP |
| 6601 | Syslog TCP |
| 6514 | Syslog TLS |

### Attach to container
```
podman exec -it syslogng bash
```

### Remove your container
```
podman stop syslogng
podman rm syslogng
```

### Source
https://docs.linuxserver.io/images/docker-syslog-ng/