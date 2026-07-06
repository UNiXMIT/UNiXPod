# smallstep CA
### Pull and Run container
```
podman pull docker.io/mallstep/step-ca:latest
podman run -itd --name smallstep \
-v /home/support/smallstep:/home/step \
-e "DOCKER_STEPCA_INIT_NAME=UNiXStep" \
-e "DOCKER_STEPCA_INIT_DNS_NAMES=localhost,$(hostname -f)" \
-e "DOCKER_STEPCA_INIT_PASSWORD=strongPassword123" \
--health-cmd 'curl -f -k https://localhost:9000/health || exit 1' \
--health-interval 10s \
--health-timeout 3s \
--health-retries 10 \
--health-start-period 10s \
docker.io/smallstep/step-ca:latest
```

### Increase Min/Max/Default Cert Duration
Minimum: 5 minutes  
Maximum: 2 years and 30 days (18240 hours)  
Default: 1 year (8760 hours)  
```
jq '.authority.claims = {
  minTLSCertDuration: "5m",
  maxTLSCertDuration: "18240h",
  defaultTLSCertDuration: "8760h"
}' /home/support/smallstep/config/ca.json > ca.json.tmp && mv ca.json.tmp /home/support/smallstep/config/ca.json
podman restart smallstep
```

### Generate Server Certificate & Key
```
mkdir /home/support/smallstep/aws
podman exec -it smallstep step ca certificate aws aws/aws.crt aws/aws.key --san "*.eu-west-2.compute.amazonaws.com" --san "*.eu-west-2.compute.internal"  --san "support" --not-after=8760h
```

### Renew Certificate
```
podman exec -it smallstep step ca renew aws/aws.crt aws/aws.key
```

### Install Root\Intermediate CA Certificate on Windows
```
certutil -user -addstore "Root" root_ca.crt
certutil -user -addstore "Root" intermediate_ca.crt
```

### Remove your container
```
podman stop smallstep
podman rm smallstep
```