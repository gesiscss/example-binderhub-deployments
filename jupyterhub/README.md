BinderHub with authentication and persistent storage (https://github.com/jupyterhub/binderhub/issues/794#issue-411794570)

```bash
kubectl create namespace bhub-test-ns

kubectl create configmap nginx-configmap --from-file=jupyterhub/nginx.conf --namespace=bhub-test-ns
kubectl apply -f nginx/nginx.yaml --namespace=bhub-test-ns

helm upgrade bhub-test jupyterhub/binderhub --version=0.2.0-6bfd93b  \
    --install --namespace=bhub-test-ns \
    -f config.yaml -f auth.yaml -f jupyterhub/config.yaml -f secret.yaml \
    --wait --force --debug --timeout=1800
```
