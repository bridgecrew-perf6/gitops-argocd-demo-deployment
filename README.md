# gitops-argocd-demo-deployment

## Deploying My App with Helm

Render chart templates locally:

```sh
helm template myapp-helm myapp-helm -f myapp-helm/values-dev.yaml
```

Install chart

```sh
helm upgrade --install myapp-helm myapp-helm -f myapp-helm/values-dev.yaml
```

Uninstall chart

```sh
helm uninstall myapp-helm
```

## Deploying My App with Argo CD

Install Argo CD

```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

or

```
kubectl create namespace argocd
kubectl apply -n argocd -f install.yaml
```

Get the default password

```sh
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

Create Argo CD Application

```sh
kubectl apply -f app.yaml
```

or

```sh
kubectl apply -f app-helm.yaml
```

Try to edit the deployment:

```sh
kubectl edit deployment -n myapp myapp-deployment
```

or

```sh
kubectl edit deployment -n myapp-helm myapp-helm-deployment
```

We'll see that Argo CD will revert back to the desired state.
