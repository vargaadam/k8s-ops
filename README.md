# Install ArgoCD

```
kustomize build .\argocd | kubectl apply -f -
```
> port forward argocd-server `kubectl port-forward <argocd-server-pod-name> <local-port>:<service-port>`


# Clusters bootstrap

## Install ArgoCD CLI

```
https://argoproj.github.io/argo-cd/cli_installation/
```

## Login

```
argocd login localhost:<local-port> --grpc-web
```
> `admin:<argocd-server-pod-name>`

> https://github.com/argoproj/argo-cd/issues/2580

## Add clusters

```
argocd cluster add `cluster-name`
```

## Bootstrap

```
kustomize build .\environments | kubectl apply -f -
```
