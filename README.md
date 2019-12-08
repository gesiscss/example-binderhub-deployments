A repo with helm chart to demonstrate different kinds of BinderHub deployments.

### Deployments

```bash
cd example-binderhub-deployments

helm repo add jupyterhub https://jupyterhub.github.io/helm-chart/
helm repo update
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
    
# with auth and persistent storage
helm upgrade --install --namespace=bhub-example-ns bhub-example helm-chart \
    -f auth.yaml -f persistent_storage.yaml -f secret.yaml \
    --wait --force --debug --timeout=360 

# to delete
helm delete --purge bhub-example
kubectl delete namespace bhub-example-ns

```

`secret.yaml` looks like:

```yaml
binderhub:
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

### Documentation

- template customization: 
 - https://binderhub.readthedocs.io/en/latest/customizing.html#template-customization
 - https://discourse.jupyter.org/t/customizing-jupyterhub-on-kubernetes/1769/18
- authentication: https://binderhub.readthedocs.io/en/latest/authentication.html
