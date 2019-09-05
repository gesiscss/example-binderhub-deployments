BinderHub with authentication and persistent storage 
(https://github.com/jupyterhub/binderhub/issues/794#issue-411794570)

```bash
helm upgrade bhub-example jupyterhub/binderhub --version=0.2.0-f746e50  \
    --install --namespace=bhub-example-ns \
    -f config.yaml -f auth.yaml -f persistent_storage/config.yaml -f secret.yaml \
    --wait --force --debug --timeout=360

# to delete
helm delete --purge bhub-example
kubectl delete namespace bhub-example-ns
```
