# Clusters bootstrap

## Install ArgoCD

```
kustomize build .\argocd | kubectl apply -f -
```

- port forward the argocd-server `kubectl port-forward <argocd-server-pod-name> <local-port>:<service-port>`

## Install ArgoCD CLI

https://argoproj.github.io/argo-cd/cli_installation/

## Login in

```
argocd login localhost:<local-port> --grpc-web
```

- **user: admin**
- **password: `kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2`**

> `--grpc-web` flag is needed because of https://github.com/argoproj/argo-cd/issues/2580

## Add git-ops repo

```
argocd repo add git@github.com:vargaadam/k8s-ops.git --insecure-ignore-host-key --ssh-private-key-path <path-to-ssh-private-key>
```

## Add clusters

```
argocd cluster add <stage-cluster-name> --name stage
argocd cluster add <prod-cluster-name> --name prod
```

## Bootstrap

```
kustomize build . | kubectl apply -f -
```

## Notes

### Secure Docker-registry

- Generate `htpasswd` with `docker run --entrypoint htpasswd registry:2.7.0 -Bbn <user> <pass>` and change the secret value.
- Create a imagePullSecret for the appropriate cluster : `kubectl create secret docker-registry regcred --docker-server=<registry.your_domain> --docker-username=<user> --docker-password=<pass>`
- registry-cred will pick up the cred and populate it to the service accounts
