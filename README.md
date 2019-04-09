Documentation:
- authentication: https://binderhub.readthedocs.io/en/latest/authentication.html
- template customization: https://binderhub.readthedocs.io/en/latest/customizing.html#template-customization

nginx app is needed for the deployment of BinderHub with `kubeadm` on bare-metal. 

Deployment:
```bash
kubectl create namespace bhub-example-ns

kubectl create configmap nginx-configmap --from-file=nginx/nginx.conf --namespace=bhub-example-ns
kubectl apply -f nginx/nginx.yaml --namespace=bhub-example-ns

# plain bhub
helm upgrade bhub-example jupyterhub/binderhub --version=0.2.0-612ade7  \
    --install --namespace=bhub-example-ns \
    -f config.yaml -f secret.yaml \
    --wait --force --debug --timeout=360

# auth
helm upgrade bhub-example jupyterhub/binderhub --version=0.2.0-612ade7  \
    --install --namespace=bhub-example-ns \
    -f config.yaml -f auth.yaml -f secret.yaml \
    --wait --force --debug --timeout=360

# auth with named servers
helm upgrade bhub-example jupyterhub/binderhub --version=0.2.0-612ade7  \
    --install --namespace=bhub-example-ns \
    -f config.yaml -f auth.yaml -f auth_with_named_servers.yaml -f secret.yaml \
    --wait --force --debug --timeout=360

# with custom templates
helm upgrade bhub-example jupyterhub/binderhub --version=0.2.0-612ade7  \
    --install --namespace=bhub-example-ns \
    -f config.yaml -f custom_templates.yaml -f secret.yaml \
    --wait --force --debug --timeout=360
```

[Deplyoment with auth and persistent storage](/persistent_storage/)

`secret.yaml` looks like:

```yaml
jupyterhub:
  hub:
    services:
      binder:
        apiToken: ""
  proxy:
    secretToken: ""
  auth:
    github:
      clientSecret: ""

registry:
  username: ""
  password: ""
```
