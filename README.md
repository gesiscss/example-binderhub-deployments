Documentation:
- template customization: 
 - https://binderhub.readthedocs.io/en/latest/customizing.html#template-customization
 - https://discourse.jupyter.org/t/customizing-jupyterhub-on-kubernetes/1769/18
- authentication: https://binderhub.readthedocs.io/en/latest/authentication.html

Deployment:
```bash
kubectl create namespace bhub-example-ns

cd example-binderhub-deployments
helm dependency update helm-chart

# plain bhub
helm upgrade --install --namespace=bhub-example-ns bhub-example helm-chart \
    -f secret.yaml \
    --wait --force --debug --timeout=360 

# auth
helm upgrade --install --namespace=bhub-example-ns bhub-example helm-chart \
    -f auth.yaml -f secret.yaml \
    --wait --force --debug --timeout=360 

# auth with named servers
helm upgrade --install --namespace=bhub-example-ns bhub-example helm-chart \
    -f auth.yaml -f auth_with_named_servers.yaml -f secret.yaml \
    --wait --force --debug --timeout=360 

# with custom templates
helm upgrade --install --namespace=bhub-example-ns bhub-example helm-chart \
    -f custom_templates.yaml -f secret.yaml \
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
