# Grafana Alloy & Loki Deployment (Helm)

This repository contains Helm values files for deploying Grafana Alloy and Loki into an existing Kubernetes cluster.

## Prerequisites

- Kubernetes cluster already running
- Grafana and Prometheus already installed in the cluster
- kubectl configured to access the cluster
- Helm v3+

## Files
```
alloy-values.yaml  
loki-values.yaml  
```
modify the placeholder `<<loki-endpoint>>` at `alloy-values.yaml` into the planned loki endpoint

## Helm Repository

Add the Grafana Helm repository:
```
helm repo add grafana https://grafana.github.io/helm-charts  
helm repo update  
```
## Install Loki

Deploy Loki using the provided values file:

```
helm upgrade --install loki grafana/loki \
  --namespace loki \
  --create-namespace \
  -f loki-values.yaml
```

## Install Grafana Alloy

Deploy Grafana Alloy using the provided values file:
```
helm upgrade --install alloy grafana/alloy \
  --namespace alloy \
  --create-namespace \
  -f alloy-values.yaml
```
## Verify
```
kubectl get pods -n loki  
kubectl get pods -n alloy  
```
Logs should now be available in Grafana under Explore using Loki as the data source.
