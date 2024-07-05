# Oracle
#### Pull and Run container
```
podman pull container-registry.oracle.com/database/free:latest
podman run -d -p 1521:1521 --name oracle -e ORACLE_PWD=strongPassword123 -e ORACLE_CHARACTERSET=AL32UTF8 container-registry.oracle.com/database/free:latest
```

#### Attach to container
```
podman exec -it oracle bash
```

### Container Details
sid: FREE  
username: sys  
password: strongPassword123  

### Connect to Database
```
podman exec -it oracle sqlplus sys/strongPassword123@//localhost:1521/FREE as sysdba
podman exec -it oracle sqlplus system/strongPassword123@//localhost:1521/FREE
podman exec -it oracle sqlplus pdbadmin/strongPassword123@//localhost:1521/FREEPDB1
```

### Create User and Schema
```
podman exec -it oracle sqlplus sys/strongPassword123@//localhost:1521/FREE as sysdba <<EOF
ALTER SESSION SET "_ORACLE_SCRIPT"=true;
CREATE USER support IDENTIFIED BY strongPassword123;
GRANT ALL PRIVILEGES TO support;
GRANT SYSDBA TO support;
GRANT SELECT ON V_\$INSTANCE TO support;
EXIT;
EOF
```

### Remove your container
```
podman stop oracle
podman rm oracle
```

### Source
[https://bit.ly/44fijqt](https://bit.ly/44fijqt)  

### ODBC Driver Setup
```
sudo dnf install [Oracle Instant Client + ODBC .rpm]
```

### ODBC Driver Location example
```
rpm -ql oracle-instantclient-odbc-*
```

### Setup ODBC Driver and DSN
```
cd /opt/oracle/instantclient_21_13
chmod +x odbc_update_ini.sh
odbc_update_ini.sh / /opt/oracle/instantclient_21_13 "Oracle 21 ODBC driver" Oracle /etc/odbc.ini
```

### odbc.ini
```
[oracle]
Description     = Oracle ODBC Connection
Driver          = /usr/lib/oracle/21/client64/lib/libsqora.so.21.1
Database        = support
Servername      = 127.0.0.1:1521/FREE
UserID          = support
```

### tnsnames.ora
Default Location - $ORACLE_HOME/network/admin    
TNS_ADMIN - Changes the directory path of Oracle Net Services configuration files from the default location of $ORACLE_HOME/network/admin   
```
oracle =
  (DESCRIPTION=
    (ADDRESS = (PROTOCOL = TCP)(HOST = xxx.xxx.xxx.xxx)(PORT = 1521)
  )
  (CONNECT_DATA =
    (SERVICE_NAME=FREE)
  )
)
```

### sqlnet.ora
Default Location - $ORACLE_HOME/network/admin
Connections to Oracle Database from clients earlier than release 10g fail with the error ORA-28040: No matching authentication protocol.  

Starting with Oracle Database 18c, the default value for the SQLNET.ALLOWED_LOGON_VERSION parameter changes from 11 in Oracle Database 12c (12.2) to 12 in Oracle Database 18c. The use of this parameter is deprecated.  

SQLNET.ALLOWED_LOGON_VERSION is now replaced with the SQLNET.ALLOWED_LOGON_VERSION_SERVER and SQLNET.ALLOWED_LOGON_VERSION_CLIENT parameters.  

```
SQLNET.ALLOWED_LOGON_VERSION_SERVER=8
SQLNET.ALLOWED_LOGON_VERSION_CLIENT=8
```

### ORA-12526, TNS:listener: all appropriate instances are in restricted mode.
```
sqlplus /nolog
conn sys as sysdba
password: strongPassword123
alter system disable restricted session;
```