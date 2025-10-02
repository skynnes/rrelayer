# rrelayer Helm Chart

This Helm chart deploys rrelayer on a Kubernetes cluster.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.0+
- PostgreSQL database (optional, can be configured via values.yaml)

## Installation

### Basic Installation

```bash
helm install rrelayer ./rrelayer
```

### With Custom Values

```bash
helm install rrelayer ./rrelayer -f custom-values.yaml
```

## Configuration

The following table lists the configurable parameters of the rrelayer chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `replicaCount` | Number of replicas | `1` |
| `image.repository` | Image repository | `ghcr.io/joshstevens19/rrelayer` |
| `image.tag` | Image tag | `latest` |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |
| `service.type` | Kubernetes service type | `ClusterIP` |
| `service.port` | Service port | `3000` |
| `ingress.enabled` | Enable ingress | `false` |
| `postgresql.enabled` | Enable PostgreSQL integration | `false` |
| `postgresql.auth.username` | PostgreSQL username | `rrelayer` |
| `postgresql.auth.password` | PostgreSQL password | `yourpassword` |
| `postgresql.auth.database` | PostgreSQL database name | `rrelayerdb` |
| `postgresql.auth.host` | PostgreSQL host | `rrelayerhost` |
| `postgresql.auth.port` | PostgreSQL port | `5432` |
| `externalSecret` | External secret name for environment variables | `""` |
| `projectPath` | Base path for project files | `/app/project` |

## Examples

### Deploy with PostgreSQL

```yaml
postgresql:
  enabled: true
  auth:
    username: "rrelayer"
    password: "securepassword"
    database: "rrelayerdb"
    host: "postgres-service"
    port: "5432"
```

### Deploy with Ingress

```yaml
ingress:
  enabled: true
  annotations:
    kubernetes.io/ingress.class: nginx
  hosts:
    - host: rrelayer.example.com
      paths:
        - /
```

### Using External Secrets

```yaml
externalSecret: "rrelayer-secrets"
```

## Uninstallation

```bash
helm uninstall rrelayer
```

## Health Checks

The chart includes liveness and readiness probes that check the `/health` endpoint on the configured service port.
