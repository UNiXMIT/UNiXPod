# NGiNX
### Pull and Run container
```
podman pull nginx:latest
podman run --name nginx -p 80:80 -p 443:443 -v /home/support/nginx:/config -e PUID=1000 -e PGID=1000 -e TZ=Europe/London -d lscr.io/linuxserver/nginx:latest
```

### --net=host
Allow the container to have direct access to the host's network.  
Instead of specifying any port mappings, set --net=host on the run command.  

### Reload nginx
```
podman exec -it nginx nginx -s reload
```

### Attach to container
```
podman exec -it nginx bash
```

### Remove your container
```
podman stop nginx
podman rm nginx
```