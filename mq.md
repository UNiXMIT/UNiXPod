# MQ
#### Pull and Run container
```
podman pull ibmcom/mq:latest

printf "yourPassword123" | podman secret create mqAdminPassword -
printf "yourPassword123" | podman secret create mqAppPassword -

podman run -d --name mq \
-e LICENSE=accept \
-e MQ_QMGR_NAME=QM1 \
-p 1414:1414 \
-p 9443:9443 \
--secret mqAdminPassword \
--secret mqAppPassword \
--health-cmd '/usr/local/bin/chkmqhealthy || exit 1' \
--health-interval 1m \
--health-timeout 30s \
--health-retries 3 \
--health-start-period 60s \
icr.io/ibm-messaging/mq:latest
```

The following queues and topics are created:  

    DEV.QUEUE.1  
    DEV.QUEUE.2  
    DEV.QUEUE.3  
    DEV.DEAD.LETTER.QUEUE - configured as the Queue Manager's Dead Letter Queue.  
    DEV.BASE.TOPIC - uses a topic string of dev/.  

Two channels are created, one for administration, the other for normal messaging:  

    DEV.ADMIN.SVRCONN - configured to only allow the admin user to connect into it. The admin user can be used with the password configured via secret.  
    DEV.APP.SVRCONN - does not allow administrative users to connect. Only the app user can connect. The password would be as configured by the secret.  

#### MQ Version Information
```
podman exec -it mq dspmqver
```

#### MQ Environment Variables
```
MQSERVER=DEV.APP.SVRCONN/TCP/<IP/HOSTNAME>(1414)
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
https://github.com/ibm-messaging/mq-container/blob/master/docs/usage.md  