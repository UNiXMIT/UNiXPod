# OpenLDAP for Enterprise Server

### Download and Execute OpenLDAP for ES script
```
curl -O https://raw.githubusercontent.com/UNiXMIT/UNiXMF/main/linux/openldap/podman.sh | bash
```

### Build and Run container
```
./podman.sh
```

### Attach to container
```
podman exec -it openldap bash
```

### DN
```
BASE = cn=Micro Focus,dc=secldap,dc=com
AuthorizedID = cn=Manager,dc=secldap,dc=com
Password = strongPassword123
```

### Remove your container
```
podman stop openldap
podman rm openldap
```

### Source
[https://github.com/UNiXMIT/UNiXMF/tree/main/linux/openldap](https://github.com/UNiXMIT/UNiXMF/tree/main/linux/openldap)