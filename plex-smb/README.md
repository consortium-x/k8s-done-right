
<img src="https://www.plex.tv/wp-content/uploads/2018/01/pmp-icon-1.png" alt="Plex Logo" width="120" height="120">

# Plex + SMB Helm Chart (`plex-smb`)

This chart deploys **Plex Media Server** with an **SMB sidecar (dperson/samba)** for media ingestion,
using Kubernetes-native primitives and rescheduling-safe storage patterns.

It is part of the **k8s-done-right** repository maintained by **Consortium X Ltd**.

---

## What This Chart Provides

- Plex Media Server (linuxserver/plex)
- SMB sidecar container for media ingestion
- Optional GPU acceleration for hardware transcoding
- Kubernetes-native rescheduling support
- RWX-aware storage model (required for reliability)

This chart **does not** bundle or redistribute Plex or Samba binaries.
It only provides Kubernetes orchestration.

---

## Prerequisites

- Kubernetes **1.19+**
- **Helm 4.x**
- RWX-capable StorageClass (CephFS, Longhorn RWX, NFS, EFS, etc.)
- PVC support enabled in the cluster
- (Optional) GPU device plugin for hardware transcoding:
  - NVIDIA, Intel, or AMD (vendor-specific)

---

## Installing the Chart

### Add the repository

```bash
helm repo add k8s-done-right https://consortium-x.github.io/k8s-done-right
helm repo update
```

### Install the chart

```bash
helm install plex-smb k8s-done-right/plex-smb \
  --namespace plex \
  --create-namespace \
  --values custom-values.yaml
```

---

## Configuration

All configuration is handled through `values.yaml`.

Key areas include:

- Plex container settings
- SMB user credentials
- RWX storage configuration
- Optional GPU resources
- Ingress / Gateway exposure (Ingress, Traefik, or Gateway API)

See `values.yaml` for the full, documented configuration surface.

---

## Manifests vs Helm

This directory includes **both**:

- `manifests/`  
  Raw Kubernetes YAML for users who want manual control

- Helm chart (`Chart.yaml`, `templates/`, `values.yaml`)  
  For repeatable, configurable deployments

The manifests and chart are functionally equivalent.

---

## Storage Requirements (Important)

RWX storage is **required** for correct behaviour.

Without RWX:
- Pods may fail to reschedule
- Plex may lose server identity
- Media access may break

This chart assumes storage is provided externally.
It does **not** install or manage storage backends.

---

## License

MIT License  
© 2025–present Consortium X Ltd

---

## Disclaimer

Plex is a registered trademark of Plex, Inc.  
This project is not affiliated with or endorsed by Plex, Inc.
