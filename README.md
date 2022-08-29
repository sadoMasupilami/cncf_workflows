# install Argo Workflows

```
kubectl create ns argo

kubectl apply -n argo -f https://github.com/argoproj/argo-workflows/releases/download/v3.3.9/quick-start-postgres.yaml

# not a good idea if reachable from outside
kubectl patch deployment \
argo-server \
--namespace argo \
--type='json' \
-p='[{"op": "replace", "path": "/spec/template/spec/containers/0/args", "value": [
"server",
"--auth-mode=server"
]}]'

kubectl -n argo port-forward deployment/argo-server 2746:2746
```

# run
see the yamls in `k8s-resources` and apply them one after the other and check on the ui what happens.

# where to go?
The best starting point is probably the excellent documentation of Argo Workflows found here: https://argoproj.github.io/argo-workflows/

You can also find a lot of examples here: https://github.com/argoproj/argo-workflows/tree/master/examples

# Install Argo Events
```
kubectl create namespace argo-events
kubectl apply -f https://raw.githubusercontent.com/argoproj/argo-events/stable/manifests/install.yaml
```