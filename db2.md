# DB2 LUW
### Pull and Run container
```
podman pull icr.io/db2_community/db2
podman run -itd --name db2 \
--privileged=true \
-p 50000:50000 \
-e LICENSE=accept \
-e DB2INSTANCE=support \
-e DB2INST1_PASSWORD=strongPassword123 \
-e DBNAME=support \
--health-cmd '/opt/ibm/db2/*/bin/db2gcf -s' \
--health-interval 30s \
--health-timeout 10s \
--health-retries 5 \
--health-start-period 120s \
icr.io/db2_community/db2
```

### Attach to container
```
podman exec -it db2 bash -c "su - support"
```

### Password Management
Change password:  
```
podman exec -it db2 passwd support
```
Turn off password expiry:  
```
podman exec -it db2 chage -M -1 -m 0 -W 0 support
```

### Connect to database and execute SQL
```
db2 CONNECT TO SUPPORT
db2 SET CURRENT SCHEMA SchemaName
db2 SELECT * FROM SUPPORT.SchemaName
```

### Connect to database and execute SQL from file
```
db2 -svtf db2.sql | tee db2.sql.out
```

t – terminated – the statements are terminated with a delimiter. The default delimiter is the semi-colon.  
v – verbose – the statement will be echoed in output prior to the result of the statement. This is extremely useful when reviewing output or troubleshooting failed statements.  
s – This option tells the command line processor to stop execution if errors occur while commands are executed in a batch file or in interactive mode.    
f – file – indicates that db2 should execute statements from a file, with the filename specified one space after the f.  

### Create new database
Using DB2 defaults:  
```
db2 create database support
```
```
db2 drop database support
```
Using specific codeset and territory:  
```
db2 create database support using codeset 1256 territory AA
```

### Remove your container
```
podman stop db2
podman rm db2
```

### Clients and Driver Downloads
https://ibm.co/3JKDGaL

### Catalog remote database on client
```
db2 catalog tcpip node <NODENAME> remote <HOSTNAME|IP_ADDRESS> server <SERVICE_NAME|PORT_NUMBER>
db2 catalog database <DBNAME> at node <NODENAME>
db2 terminate
db2 connect to <DBNAME> user <USERNAME> using <PASSWORD>
```
NODENAME - A local nickname you can set for the computer that has the database you want to catalog.  
DBNAME - Name of remote database to catalog.  
```
db2 list node directory
db2 list database directory
db2 uncatalog node <NODENAME>
db2 uncatalog database <DBNAME>
db2 terminate
```

### Install ODBC Driver (cmd as Admin on Windows only)
```
db2cli install -setup
```

### odbcinst.ini
```
[IBM DB2 ODBC DRIVER]
Description = DB2 Driver
Driver = <instance_path>/sqllib/lib64/libdb2o.so
fileusage=1
dontdlclose=1
```

### odbc.ini
```
[db2]
Driver = IBM DB2 ODBC DRIVER
Database = support
Server = localhost
Port = 50000
UID = support
PWD = strongPassword123
```

### Source
https://ibm.co/3JuuQga  