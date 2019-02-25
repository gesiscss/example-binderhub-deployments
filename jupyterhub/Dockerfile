# https://github.com/jupyterhub/zero-to-jupyterhub-k8s/tree/c83896f/images/hub
# https://hub.docker.com/r/jupyterhub/k8s-hub/tags/
# tag c83896f is from https://jupyterhub.github.io/helm-chart/binderhub-0.2.0-6bfd93b.tgz
FROM jupyterhub/k8s-hub:c83896f

USER root
COPY templates /srv/jhub_custom_templates
USER ${NB_USER}