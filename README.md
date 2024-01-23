## Test your config

Server (Reality)
```
docker run -it -p 443:443 --name xray-server --rm \
    -v $(pwd)/etc/xray:/etc/xray/ \
    teddysun/xray
```
Client
```
docker run -d -p 3128:3128 --name xray --restart unless-stopped \
    -v $(pwd)/client/etc/xray:/etc/xray/ \
    teddysun/xray
```


## Deploy to your Kubernetes

Install
```
k create ns xray-vpn
kubens xray-vpn
kubectl create secret generic vpn-config \
  --from-file=etc/xray/config.json \
  -o yaml --dry-run=client | kubeseal -o yaml > manifests/k8s/sealed-config-secret.yaml
kubectl create --save-config -f manifests/k8s/sealed-config-secret.yaml -n xray-vpn
kubectl create --save-config -f manifests/k8s/daemonset.yaml -n xray-vpn
```

Update
```
k apply -f xray-config.yaml
k rollout restart deploy
```

Remove
```
k delete ns xray-vpn
```
