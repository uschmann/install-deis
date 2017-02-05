# Install deis-workflow

## Add deis rpo to helm
```bash
helm repo add deis https://charts.deis.com/workflow
```

## Generate config.yaml
```bash
helm inspect values deis/workflow >> config.yaml
```

## Install deis
```bash
helm install -f config.yaml deis/workflow --namespace=deis
```

## Get coffe and watch the pods spawning
```bash
kubectl get pods -w
```

## Get router config
```bash
kubectl get services --namespace=deis deis-router -o yaml >> router.config
```

## Apply router config
```bash
kubectl apply -f router.config
```

## Register the admin user
```bash
deis register http://deis.$DEIS_HOST.nip.io
```

## Change registration mode to admin_only
```bash
kubectl --namespace=deis patch deployments deis-controller -p '{"spec":{"template":{"spec":{"containers":[{"name":"deis-controller","env":[{"name":"REGISTRATION_MODE","value":"admin_only"}]}]}}}}'
```

## Add ssh key
```bash
deis keys:add
```
