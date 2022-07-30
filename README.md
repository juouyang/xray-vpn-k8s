## Test your config

Server
```
docker run -it -p 9000:9000 --name xray-server --rm \
    -v $(pwd)/etc/xray:/etc/xray/ \
    teddysun/xray
```
Client
```
docker run -d -p 3128:3128 -p 1080:1080 --name xray --restart unless-stopped \
    -v $(pwd)/client/etc/xray:/etc/xray/ \
    teddysun/xray
```


## Deploy to your Kubernetes

Install
```
k create ns xray-vpn
# export do="--dry-run=client -o yaml"
# k create configmap vpn-config --from-file=etc/xray/config.json $do > xray-config.yaml
k create --save-config -f xray-config.yaml
k create --save-config -f xray-deployment.yaml
k create --save-config -f xray-service.yaml
k create --save-config -f xray-hpa.yaml
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
