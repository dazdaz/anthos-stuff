# anthos_stuff

# Excellent example of using Anthos Connect gateway in a multi-cloud setup
# https://twitter.com/rseroter/status/1376925282079100936

```
multi-cloudbuid.yaml
steps:
- name: 'gcr.io/cloud-builders/gcloud'
  entrypoint: /bin/sh
  id: Deploy to AKS cluster
  args:
  - '-c'
  - |
    set -x && \
    export KUBECONFIG="$(pwd)/gateway-kubeconfig" && \
    gcloud beta container hub memberships get-credentials cluster-mine-aks-cluster && \
    kubectl --kubeconfig gateway-kubeconfig apply -f generic-deployment.yaml
- name: 'gcr.io/cloud-builders/gcloud'
  entrypoint: /bin/sh
  id: Deploy to kind cluster
  args:
  - '-c'
  - |
  set -x && \
  export KUBECONFIG="$(pwd)/gateway/kubeconfig" && \
  gcloud beta container hub memberships get-credentials cluster-mine-kind-cluster && \
  kubectl --kubeconfig gateway-kubeconfig apply -f generic-deployment.yaml
```
