# MYSQL

### Pull and Run container
```
podman pull container-registry.oracle.com/mysql/community-server:latest
podman run -d --name=mysql \
-p 3306:3306 \
-e "MYSQL_ROOT_PASSWORD=strongPassword123" \
-e "MYSQL_DATABASE=support" \
-e "MYSQL_USER=support" \
-e "MYSQL_PASSWORD=strongPassword123" \
--health-cmd 'mysqladmin ping' \
--health-interval 10s \
--health-timeout 5s \
--health-retries 3 \
--health-start-period 30s \
container-registry.oracle.com/mysql/community-server:latest
```

### Attach to container
```
podman exec -it mysql mysql -uroot -pstrongPassword123
```

### Remove container
```
podman stop mysql
podman rm mysql
```

### Source
https://bit.ly/44fijqt
