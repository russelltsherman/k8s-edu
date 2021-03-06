# istio install

download (0.7.1):

```sh
wget https://github.com/istio/istio/releases/download/0.7.1/istio-0.7.1-linux.tar.gz
tar -xzvf istio-0.7.1-linux.tar.gz
cd istio-0.7.1
echo 'export PATH="$PATH:/home/ubuntu/istio-0.7.1/bin"' >> ~/.profile
```

with no mutual TLS authentication

```sh
kubectl apply -f install/kubernetes/istio.yaml
```

or with mutual TLS authentication

```sh
kubectl apply -f install/kubernetes/istio-auth.yaml
```

Example app (from istio)

```sh
kubectl edit svc istio-ingress -n istio-system # change loadbalancer to nodeport (or use hostport)
export PATH="$PATH:/home/ubuntu/istio-0.7.1/bin"
kubectl apply -f <(istioctl kube-inject --debug -f samples/bookinfo/kube/bookinfo.yaml)
```

## Traffic management

Add default route to v1:

```sh
istioctl create -f samples/bookinfo/routing/route-rule-all-v1.yaml
```

Route traffic to v2 if rule matches

```sh
istioctl replace -f samples/bookinfo/routing/route-rule-reviews-test-v2.yaml
```

Route 50% of traffic between v1 and v3:

```sh
istioctl replace -f samples/bookinfo/routing/route-rule-reviews-50-v3.yaml
```

## Distributed tracing

Enable zipkin:

```sh
kubectl apply -f install/kubernetes/addons/zipkin.yaml
```

Enable Jaeger:

```sh
kubectl delete -f install/kubernetes/addons/zipkin.yaml # if zipkin was installed, delete it first
kubectl apply -n istio-system -f https://raw.githubusercontent.com/jaegertracing/jaeger-kubernetes/master/all-in-one/jaeger-all-in-one-template.yml

```
