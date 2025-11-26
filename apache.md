# Apache httpd Web Server
### Pull and Run container
```
podman pull nginx:latest
podman run --name apache -p 80:80 -p 443:443 -v /home/support/apache/htdocs:/usr/local/apache2/htdocs -v /home/support/apache/sites:/usr/local/apache2/conf/sites -d httpd:latest
```

### --net=host
Allow the container to have direct access to the host's network.  
Instead of specifying any port mappings, set --net=host on the run command.  

### Configure the Virtual Host Directory Path
```
podman exec -it apache sh -c 'echo "IncludeOptional conf/sites/*.conf" >> conf/httpd.conf'
```

### Reload Apache
```
podman exec -it apache apachectl graceful
```

### Attach to container
```
podman exec -it apache bash
```

### Remove your container
```
podman stop apache
podman rm apache
```