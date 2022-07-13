```
k create ns xray-vpn
k create --save-config -f xray-config.yaml
k create --save-config -f xray-deployment.yaml
k create --save-config -f xray-service.yaml
k create --save-config -f xray-hpa.yaml
```