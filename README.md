# iac-flux-prefect-server
Flux Configuration for Prefect Server


## Developer Guide
To test the changes, ensure that you are on your developer machine and that the context is set correctly to your local instance please amend the following script to use the target branch:

```bash
kubectl create namespace prefect
flux create source git prefect --url="https://github.com/lsc-sde/iac-flux-prefect-server" --branch=main --namespace=prefect
flux create kustomization prefect-cluster-config --source="GitRepository/prefect" --namespace=prefect --path="./cluster/local" --interval=1m --prune=true --health-check-timeout=10m --wait=false
flux create kustomization prefect-sources --source="GitRepository/prefect" --namespace=prefect --path="./sources" --interval=1m --prune=true --health-check-timeout=10m --wait=false
```

This should in turn deploy all of the resulting resources on your local cluster.