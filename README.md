Documentation:
- authentication: https://binderhub.readthedocs.io/en/latest/authentication.html
- template customization: https://binderhub.readthedocs.io/en/latest/customizing.html#template-customization

Deployment:
```bash
kubectl create namespace bhub-example-ns

# plain bhub
helm upgrade bhub-example jupyterhub/binderhub --version=0.2.0-f746e50  \
    --install --namespace=bhub-example-ns \
    -f config.yaml -f secret.yaml \
    --wait --force --debug --timeout=360

# auth
helm upgrade bhub-example jupyterhub/binderhub --version=0.2.0-f746e50  \
    --install --namespace=bhub-example-ns \
    -f config.yaml -f auth.yaml -f secret.yaml \
    --wait --force --debug --timeout=360

# auth with named servers
helm upgrade bhub-example jupyterhub/binderhub --version=0.2.0-f746e50  \
    --install --namespace=bhub-example-ns \
    -f config.yaml -f auth.yaml -f auth_with_named_servers.yaml -f secret.yaml \
    --wait --force --debug --timeout=360

# with custom templates
helm upgrade bhub-example jupyterhub/binderhub --version=0.2.0-f746e50  \
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
      clientId: ""
      clientSecret: ""

registry:
  username: ""
  password: ""

config:
  GitHubRepoProvider:
    access_token: ""
```
