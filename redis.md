# Redis
### Pull and Run container
```
podman pull docker.io/redis
podman run -d --name redis \
-p 6379:6379 \
--health-cmd 'redis-cli ping || exit 1' \
--health-interval 10s \
--health-timeout 3s \
--health-retries 10 \
--health-start-period 10s \
docker.io/redis
```

### Attach to container
```
podman exec -it redis bash
```

### Remove your container
```
podman stop redis
podman rm redis
```

### Source
https://dockr.ly/3HrYkJi