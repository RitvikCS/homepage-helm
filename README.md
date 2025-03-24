# Homepage Helm Chart

This repository contains a Helm chart for deploying the [Homepage](https://gethomepage.dev) dashboard application. This is still a work in progress and made for learning Helm. Please test out and let me know if there are any issues.

## Usage

### Add the Helm Repository

```bash
helm repo add homepage https://ritvikcs.github.io/homepage-helm
helm repo update
```

### Install the Chart

```bash
helm install my-homepage homepage/homepage
```

## Configuration

The following table lists the configurable parameters of the Homepage chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `replicaCount` | Number of replicas to deploy | `1` |
| `image.repository` | Image repository | `ghcr.io/gethomepage/homepage` |
| `image.tag` | Image tag | `latest` |
| `image.pullPolicy` | Image pull policy | `Always` |
| `service.type` | Kubernetes Service type | `ClusterIP` |
| `service.port` | Service port | `3000` |
| `ingress.enabled` | Enable ingress | `true` |
| `ingress.hosts[0].host` | Hostname for the ingress | `homepage.my.network` |
| `config.kubernetes.mode` | Kubernetes integration mode | `cluster` |
| `config.services` | Homepage services configuration | See values.yaml |
| `config.bookmarks` | Homepage bookmarks configuration | See values.yaml |
| `config.widgets` | Homepage widgets configuration | See values.yaml |
| `env` | Environment variables | See values.yaml |
| `resources` | CPU/Memory resource requests/limits | `{}` |

## Customization

To override the default values, create a `values.yaml` file and specify the values you wish to change:

```bash
helm install my-homepage homepage/homepage -f values.yaml
```

### Services Configuration

Homepage services can be configured using the `config.services` parameter. Here's an example:

```yaml
config:
  services: |
    - Mealie Group:
        - Mealie:
            href: http://localhost:9000
            description: Mealie
    - My Second Group:
        - Homepage:
            href: https://gethomepage.dev
            description: Modern dashboard for your services
```

### Widgets Configuration

Homepage widgets can be configured using the `config.widgets` parameter:

```yaml
config:
  widgets: |
    - kubernetes:
        cluster:
          show: true
          cpu: true
          memory: true
          showLabel: true
          label: "cluster"
        nodes:
          show: true
          cpu: true
          memory: true
          showLabel: true
    - resources:
        backend: resources
        expanded: true
        cpu: true
        memory: true
        network: default
    - search:
        provider: duckduckgo
        target: _blank
```


## Contributing

Contributions are welcome! Please feel let me know if there are any changes that should be made.