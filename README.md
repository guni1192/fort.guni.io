# fort


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
