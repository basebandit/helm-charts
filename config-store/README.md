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
