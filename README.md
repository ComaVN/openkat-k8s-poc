# openkat-k8s-poc
PoC for deploying OpenKAT in Kubernetes


To get it to work locally, use k3s.

It uses the [CloudNativePG k8s operator](https://cloudnative-pg.io/):
```
kubectl apply -f https://raw.githubusercontent.com/cloudnative-pg/cloudnative-pg/release-1.21/releases/cnpg-1.21.1.yaml
```

It runs in namespace `openkat-k8s-poc`:
```
kubectl config use-context k3d-mycluster
kubectl create namespace openkat-k8s-poc
kubectl config set-context --current --namespace=openkat-k8s-poc
```

Apply the manifests:
```
kubectl apply -k overlays/local
```

Open a port forward the the main Rocky GUI service:
```
kubectl port-forward svc/openkat-rocky-svc 8000
```

Rocky is now available at <http://localhost:8000/>. Log in as `superuser@localhost`. The password is in [the `openkat-rocky` secret](overlays/local/secret-rocky.yaml).
