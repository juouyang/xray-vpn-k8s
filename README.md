```
k create ns xray-vpn
# export do="--dry-run=client -o yaml"
# k create configmap vpn-config --from-file=config.json $do > xray-config.yaml
k create --save-config -f xray-config.yaml
k create --save-config -f xray-deployment.yaml
k create --save-config -f xray-service.yaml
k create --save-config -f xray-hpa.yaml
```