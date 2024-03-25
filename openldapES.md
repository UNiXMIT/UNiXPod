# OpenLDAP for Enterprise Server

### Download OpenLDAP for ES script
```
curl -o openldap.sh https://raw.githubusercontent.com/UNiXMIT/UNiXMF/main/linux/openldap/podman.sh
chmod +x openldap.sh
```

### Build and Run container
```
./openldap.sh
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