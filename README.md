# Clusters bootstrap

## Install ArgoCD

```
kustomize build .\argocd | kubectl apply -f -
```

## Install ArgoCD CLI


https://argoproj.github.io/argo-cd/cli_installation/


## Login in

```
argocd login localhost:<local-port> --grpc-web
```
> `admin:<argocd-server-pod-name>`

> https://github.com/argoproj/argo-cd/issues/2580

## Add git-ops repo

 ```
 argocd repo add <git-ssh-url> --insecure-ignore-host-key --ssh-private-key-path <path-to-ssh-private-key>
 ```

## Add clusters

```
argocd cluster add `cluster-name`
```

## Bootstrap

```
kustomize build .\environments | kubectl apply -f -
```

