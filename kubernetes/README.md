# Cluster
## Create local cluster
```shell
kind create cluster --config kind-cluster.yml
kubectl cluster-info --context kind-plausible-local # Set context
```

## Create Remote cluster
```
kops toolbox template --template ./kops-cluster.yml  --set domain_name=DOMAIN_NAME | kops create -f -
```

# Deploying
## Create Resource
```shell
# Order is important
kubectl create -f resources/namespace.yml
kubectl create -f resources/config.yml
kubectl create -f resources/postgres.yml
kubectl create -f resources/mail.yml
kubectl create -f resources/clickhouse.yml
kubectl create -f resources/plausible.yml
kubectl create -f resources/caddy.yml
```