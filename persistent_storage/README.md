BinderHub with authentication and persistent storage (https://github.com/jupyterhub/binderhub/issues/794#issue-411794570)

```bash
kubectl create namespace bhub-example-ns

kubectl create configmap nginx-configmap --from-file=persistent_storage/nginx.conf --namespace=bhub-example-ns
kubectl apply -f nginx/nginx.yaml --namespace=bhub-example-ns

helm upgrade bhub-example jupyterhub/binderhub --version=0.2.0-612ade7  \
    --install --namespace=bhub-example-ns \
    -f config.yaml -f auth.yaml -f persistent_storage/config.yaml -f secret.yaml \
    --wait --force --debug --timeout=360

# with keycloak
helm upgrade bhub-example jupyterhub/binderhub --version=0.2.0-612ade7  \
    --install --namespace=bhub-example-ns \
    -f config.yaml -f auth.yaml -f persistent_storage/config.yaml -f persistent_storage/config_keycloak.yaml \
    -f secret.yaml -f persistent_storage/secret_keycloak.yaml \
    --wait --force --debug --timeout=360

# to delete
kubectl delete -f nginx/nginx.yaml --namespace=bhub-example-ns
kubectl delete configmap nginx-configmap --namespace=bhub-example-ns
helm delete --purge bhub-example
kubectl delete namespace bhub-example-ns
```
