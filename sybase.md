# Sybase

### Pull and Run container
```
podman pull superbeeeeeee/docker-sybase
podman run -d -it --name sybase -e SA_PASSWORD=strongPassword123 -e DATABASE=support -p 5000:5000 superbeeeeeee/docker-sybase
```

### User
SYBASE_USER	            sa  
SYBASE_PASSWORD	        strongPassword123  
SYBASE_DB	            support  

### Attach to container
```
podman exec -it sybase bash
```

### Remove your container
```
podman stop sybase
podman rm sybase
```

### Sybase Environment
```
podman cp sybase:/opt/sap /home/
export PATH="/home/sap/OCS-16_0/bin":$PATH
export LD_LIBRARY_PATH="/home/sap/OCS-16_0/lib:/home/sap/OCS-16_0/lib3p64:/home/sap/OCS-16_0/lib3p":$LD_LIBRARY_PATH
export SYBASE=/home/sap
isql -U sa -P strongPassword123 -S SYBASE -I /home/sap/interfaces
```

### Source
https://bit.ly/3wkNtQu  