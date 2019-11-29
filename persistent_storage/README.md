BinderHub with authentication and persistent storage 
(https://github.com/jupyterhub/binderhub/issues/794#issue-411794570)

```bash
helm upgrade --install --namespace=bhub-example-ns bhub-example helm-chart \
    -f auth.yaml -f persistent_storage/config.yaml -f secret.yaml \
    --wait --force --debug --timeout=360 

# to delete
helm delete --purge bhub-example
kubectl delete namespace bhub-example-ns

```
