Documentation:
- authentication: https://binderhub.readthedocs.io/en/latest/authentication.html
- template customization: https://binderhub.readthedocs.io/en/latest/customizing.html#template-customization

nginx app is needed for the deployment of BinderHub with `kubeadm` on bare-metal. 

Deployment:
```bash
kubectl create namespace bhub-test-ns

kubectl create configmap nginx-configmap --from-file=nginx/nginx.conf --namespace=bhub-test-ns
kubectl apply -f nginx/nginx.yaml --namespace=bhub-test-ns

# plain bhub
helm upgrade bhub-test jupyterhub/binderhub --version=0.2.0-6bfd93b  \
    --install --namespace=bhub-test-ns \
    -f config.yaml -f secret.yaml \
    --wait --force --debug --timeout=1800

# auth
helm upgrade bhub-test jupyterhub/binderhub --version=0.2.0-6bfd93b  \
    --install --namespace=bhub-test-ns \
    -f config.yaml -f auth.yaml -f secret.yaml \
    --wait --force --debug --timeout=1800

# auth with named servers
helm upgrade bhub-test jupyterhub/binderhub --version=0.2.0-6bfd93b  \
    --install --namespace=bhub-test-ns \
    -f config.yaml -f auth.yaml -f auth_with_named_servers.yaml -f secret.yaml \
    --wait --force --debug --timeout=1800

# with custom templates
helm upgrade bhub-test jupyterhub/binderhub --version=0.2.0-6bfd93b  \
    --install --namespace=bhub-test-ns \
    -f config.yaml -f custom_templates.yaml -f secret.yaml \
    --wait --force --debug --timeout=1800
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
