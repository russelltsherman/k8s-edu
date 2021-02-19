# Network policy

## ingress

```sh
kubectl create -f nginx.yml
kubectl create -f networkpolicy-isolation.yml
kubectl create -f networkpolicy-nginx.yml
```

```sh
kubectl run -it --rm -l app=access-nginx --image busybox busybox
```

## egress

```sh
kubectl replace -f networkpolicy-isolation.yml
kubectl create -f networkpolicy-allow-egress.yml
```
