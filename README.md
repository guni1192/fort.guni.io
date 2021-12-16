# fort

Guni's kubernetes app

## Addons

- Flux
- Grafana
- Prometheus
- Tekton (TBD)
- MetalLB (TBD)
- Nginx Ingress (TBD)
- Vault (TBD)

## Monitoring

```
flux create source git monitoring \
  --interval=30m \
  --url=https://github.com/guni1192/fort.guni.io.git \
  --branch=main
```

```
flux create kustomization monitoring-stack \
  --interval=1h \
  --prune=true \
  --source=monitoring \
  --path="./dev/monitoring/kube-prometheus-stack" \
  --health-check="Deployment/kube-prometheus-stack-operator.monitoring" \
  --health-check="Deployment/kube-prometheus-stack-grafana.monitoring"
```

Install Flux Grafana dashboards

```
flux create kustomization monitoring-config \
  --interval=1h \
  --prune=true \
  --source=monitoring \
  --path="./dev/monitoring/monitoring-config"
```


## Development

```
minikube start --nodes 3 --driver=docker
```
