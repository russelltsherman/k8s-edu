# hello minikube

## start minikube instance

```sh
[I] ➜ minikube start

😄  minikube v1.12.1 on Darwin 10.15.5
✨  Using the virtualbox driver based on user configuration
👍  Starting control plane node minikube in cluster minikube
🔥  Creating virtualbox VM (CPUs=4, Memory=8192MB, Disk=20000MB) ...
🐳  Preparing Kubernetes v1.18.4 on Docker 19.03.12 ...
🔎  Verifying Kubernetes components...
🌟  Enabled addons: default-storageclass, storage-provisioner
🏄  Done! kubectl is now configured to use "minikube"
```

## verify status ready

```sh
[I] ➜ kubectl get nodes

NAME STATUS ROLES AGE VERSION
minikube Ready master 10h v1.18.4
```

## create hello minikube deployment

```sh
[I] ➜ kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.10

deployment.apps/hello-minikube created
```

## verify hello minikube deployment

```sh
[I] ➜ kubectl get deployments

NAME READY UP-TO-DATE AVAILABLE AGE
hello-minikube 0/1 1 0 19s
```

## create hello minikube service

```sh
[I] ➜ kubectl expose deployment hello-minikube --type=NodePort --port=8080

service/hello-minikube exposed
```

## verify hello minikube service

```sh
[I] ➜ kubectl get services

NAME             TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
hello-minikube   NodePort    10.96.26.126   <none>        8080:30947/TCP   7s
kubernetes       ClusterIP   10.96.0.1      <none>        443/TCP          60s
```

## view hello minikube front end

```sh
[I] ➜ open $(minikube service hello-minikube --url)
```

## expose docker in minikube to local shell

```sh
[I] ➜ minikube docker-env

export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://192.168.99.110:2376"
export DOCKER_CERT_PATH="/Users/russellsherman/.minikube/certs"
export MINIKUBE_ACTIVE_DOCKERD="minikube"

# To point your shell to minikube's docker-daemon, run:
# eval $(minikube -p minikube docker-env)
```
