# Oodle Kubernetes Helm Charts

## Add Oodle Helm repo

```bash
helm repo add oodle https://oodle-ai.github.io/helm-charts
```

## Get latest charts from Oodle Helm repo

```bash
helm repo update oodle
```

## Search charts on Oodle Helm repo

```bash
helm search repo oodle
```

## Remove Oodle Helm repo

```bash
helm repo remove oodle
```

## Charts

### k8s-monitoring

#### Send metrics to Oodle endpoint 

Create a `values.yaml` file

```bash
cat >> values.yaml << EOF
cluster:
  name: my-cluster

externalServices:
  prometheus:
    host: '{OODLE_ENDPOINT}'
    apiKey: '{OODLE_API_KEY}'
    writeEndpoint: '/v1/prometheus/{OODLE_INSTANCE}/write'
EOF

helm install oodle-k8s-monitoring --atomic --timeout 300s oodle/k8s-monitoring --values values.yaml --namespace oodle-monitoring --create-namespace
```

#### Doublewrite to Oodle

Create a `values.yaml` file

```bash
cat > values.yaml << EOF
cluster:
  name: my-cluster

externalServices:
  prometheus:
    host: '{DEFAULT_ENDPOINT}'
    basicAuth:
      username: '{USERNAME}'
      password: '{PASSWORD}'
    oodle:
      host: '{OODLE_ENDPOINT}'
      apiKey: '{OODLE_API_KEY}'
      writeEndpoint: '/v1/prometheus/{OODLE_INSTANCE}/write'
EOF

helm install oodle-k8s-monitoring --atomic --timeout 300s oodle/k8s-monitoring --values values.yaml --namespace oodle-monitoring --create-namespace
```
