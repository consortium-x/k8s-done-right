# k8s-done-right

**Opinionated but Kubernetes-native Helm charts**, maintained by **Consortium X Ltd**,  
focused on **correctness**, **rescheduling safety**, and **production-grade primitives**.

This repository exists because many Helm charts optimise for *quick installs* rather than
*correct behaviour once things inevitably change*.

Kubernetes is a distributed system.  
Nodes fail. Pods move. Storage reattaches.  
These charts are written with that reality in mind.

---

## What This Repository Is

- A collection of **Helm charts that respect Kubernetes fundamentals**
- Charts designed to **survive rescheduling**, not fight it
- Storage, networking, and hardware usage expressed **explicitly**
- Minimal assumptions about cluster layout
- Safe defaults, with **intentional configuration required for sharp edges**

---

## Design Principles

### Kubernetes-Native First
- Pods are ephemeral
- Nodes are replaceable
- Storage must tolerate movement
- Scheduling decisions belong to the scheduler

### Explicit Over Implicit
- Hardware access (GPU, accelerators) is opt-in
- Storage semantics (RWO vs RWX) are deliberate
- Runtime behaviour is visible in values, not hidden in templates

### Rescheduling Is a Feature
- Charts are written assuming pods *will* move
- RWX storage is used where identity and continuity matter
- Node pinning is avoided unless there is a clear technical reason

---

## Repository Structure

```text
charts/
  plex/
    Chart.yaml
    values.yaml
    templates/
```

Each chart is:
- Self-contained
- Documented in its own `README.md`
- Versioned independently
- Licensed under MIT unless stated otherwise

---

## Current Charts

### Plex Media Server + SMB Sidecar
- Kubernetes-native Plex deployment
- SMB sidecar for media ingestion
- RWX storage for rescheduling safety
- Optional GPU acceleration (NVENC / QSV / VAAPI)
- Designed for single-node *and* multi-node clusters

More charts will be added over time as they are proven in real clusters.

---

## Licensing

All charts in this repository are released under the **MIT License**, unless explicitly stated otherwise.

This repository **does not redistribute or modify upstream software**.  
It provides Kubernetes orchestration only.

Upstream projects retain their own licenses and trademarks.

---

## About Consortium X

**Consortium X Ltd** is a UK-based engineering and technology company focused on
distributed systems, secure infrastructure, and production-grade delivery.

This repository reflects how we run Kubernetes internally —  
not how it looks in a blog post.

---

## Status

- ✅ Actively maintained
- ✅ Used in production clusters


If something breaks, it’s because an assumption changed —  
not because it was papered over.
