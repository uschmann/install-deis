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

## Register the admin user
```bash
deis register http://deis.$DEIS_HOST.nip.io
``
