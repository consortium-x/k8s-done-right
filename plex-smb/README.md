# Plex Helm Chart

Deploys Plex Media Server with SMB sidecar for media ingestion.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+
- PVC support for storage classes
- GPU device plugin (optional, for hardware transcoding)

## Installing the Chart

```bash
# Add the chart repository
helm repo add plex-charts https://your-chart-repo/

# Install with release name "plex"
helm install plex plex-charts/plex \
  --namespace plex \
  --create-namespace \
  --values custom-values.yaml