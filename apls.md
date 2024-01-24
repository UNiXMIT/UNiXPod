# AutoPass License Server
### Pull and Run container
```
podman pull mfsharedtech/apls:latest
podman run -d --name apls --privileged=true -p 5814:5814 -e EULA='true' -e TIME_ZONE=GMT mfsharedtech/apls:latest
```

### Attach to container
```
podman exec -it apls bash
```

### Remove your container
```
podman stop apls
podman rm apls
```

### Source
https://dockr.ly/3MRFDAr