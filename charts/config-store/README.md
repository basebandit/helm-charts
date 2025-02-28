# Config Store Helm Chart

The `config-store` Helm chart facilitates the deployment of a centralized configuration storage solution within a Kubernetes cluster. It ensures consistent and efficient management of application configurations across various environments.

## Prerequisites

- Kubernetes 1.16+
- Helm 3.0+

## Installation

To deploy the `config-store` chart with the release name `my-config-store`:

```sh
helm repo add basebandit https://basebandit.github.io/helm-charts/
helm repo update
helm install my-config-store basebandit/config-store
```

## Customization
The config-store chart can be customized using a values.yaml file to override default settings.

Example custom_values.yaml:
```yaml
replicaCount: 3

image:
  repository: baseband1t/config-store
  tag: 1.0.0
  pullPolicy: Always

service:
  type: LoadBalancer
  port: 9090

resources:
  limits:
    cpu: 1
    memory: 512Mi
  requests:
    cpu: 500m
    memory: 256Mi

nodeSelector:
  environment: production

tolerations:
  - key: "dedicated"
    operator: "Equal"
    value: "config-store"
    effect: "NoSchedule"
```

To deploy the chart with custom configurations:

```bash
helm install my-config-store basebandit/config-store -f custom_values.yaml
```

## Overriding Default Values
You can override values without modifying `values.yaml` by using the `--set` flag:

```bash
helm install my-config-store basebandit/config-store \
  --set replicaCount=3 \
  --set service.port=9090 \
  --set image.tag=2.0.0
```

For multiple overrides:

```bash
helm install my-config-store basebandit/config-store \
  --set image.repository=baseband1t/config-store \
  --set image.pullPolicy=Always \
  --set nodeSelector.environment=production
```

## Upgrading the Chart
To upgrade the existing deployment with modified configurations:

```bash
helm upgrade my-config-store basebandit/config-store -f custom_values.yaml
```

If you need to update only a few values:

```bash
helm upgrade my-config-store basebandit/config-store \
  --set image.tag=2.1.0 \
  --set resources.limits.cpu=750m
```

## Uninstallation
To remove the config-store deployment:

```bash
helm uninstall my-config-store
```

This command deletes all Kubernetes components associated with the chart and removes the release from Helm.

