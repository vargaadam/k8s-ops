# Install ArgoCD

```
kustomize build .\cluster-components\ci-cd\argocd | kubectl apply -f -
```

# Clusters bootstrap

## Infra

```
kubectl apply -f .\environments\infra\app-generator.yaml
```
