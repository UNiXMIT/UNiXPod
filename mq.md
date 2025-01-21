# MQ
#### Pull and Run container
```
podman pull ibmcom/mq:latest
podman run -d --name mq \
-e LICENSE=accept \
-e MQ_QMGR_NAME=QM1 \
-p 1414:1414 \
-p 9443:9443 \
-e MQ_ADMIN_PASSWORD=yourPassword123 \
-e MQ_APP_PASSWORD=yourPassword123 \
--health-cmd '/usr/local/bin/chkmqhealthy || exit 1' \
--health-interval 1m \
--health-timeout 30s \
--health-retries 3 \
--health-start-period 60s \
icr.io/ibm-messaging/mq:latest
```

#### MQ Version Information
```
podman exec -it mq dspmqver
```

#### Remove your container
```
podman stop mq
podman rm mq
```

#### MQ Client Downloads
https://developer.ibm.com/articles/mq-downloads/  
Windows - https://ibm.biz/IBM-MQC-Redist-Win64zip  
Linux - https://ibm.biz/IBM-MQC-Redist-LinuxX64targz  

#### Connection Test
https://www.ibm.com/support/pages/using-telnet-test-connectivity-between-mq-client-and-mq-server

#### Source
https://ibm.co/43xwS82