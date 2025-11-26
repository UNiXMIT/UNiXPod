# Keycloak
#### Pull and Run container
```
podman pull quay.io/keycloak/keycloak:latest
podman run -d -it --name keycloak -p 8080:8080 -e KC_BOOTSTRAP_ADMIN_USERNAME=admin -e KC_BOOTSTRAP_ADMIN_PASSWORD=strongPassword123 quay.io/keycloak/keycloak:latest start-dev
```

### Attach to container
```
podman exec -it keycloak bash
```

### Container Details
```
username: admin   
password: strongPassword123 
```

### Remove container
```
podman stop keycloak
podman rm keycloak
```

### Source
[https://www.keycloak.org/getting-started/getting-started-docker](https://www.keycloak.org/getting-started/getting-started-docker)  