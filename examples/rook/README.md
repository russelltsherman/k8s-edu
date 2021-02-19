# Rook

Examples from <https://github.com/rook/rook/tree/master/cluster/examples/kubernetes>

## Install rook

```sh
kubectl create -f common.yaml
kubectl create -f operator.yaml
kubectl create -f cluster.yaml
```

## Rook tools

```sh
kubectl create -f toolbox.yaml
```

## File Storage

```sh
kubectl create -f filesystem.yaml
```

## MySQL demo

```sh
kubectl create -f mysql-demo.yaml
```

## Object Storage

```sh
kubectl create -f objectstore.yaml
```

Create user:

```sh
radosgw-admin user create \
    --uid rook-user \
    --display-name "A rook rgw User" \
    --rgw-realm=my-store \
    --rgw-zonegroup=my-store
```

Export variables

```sh
export AWS_HOST=
export AWS_ENDPOINT=
export AWS_ACCESS_KEY_ID=
export AWS_SECRET_ACCESS_KEY=
```
