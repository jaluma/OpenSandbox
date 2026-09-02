---
title: Jaluma Fork Releases
description: Image and Helm release reference for the Jaluma OpenSandbox fork.
---

# Jaluma Fork Releases

This page documents the release outputs published by the `jaluma/OpenSandbox`
fork. The fork keeps upstream component versions when the component was not
changed, and uses the next component version when the fork contains changes to
that component.

## Current Image Matrix

The all-images workflow publishes multi-architecture images to GHCR:

| Component | Image tag | Reason |
| --- | --- | --- |
| Controller | `v0.2.0` | Unchanged component version |
| Egress | `v1.1.7` | Upstream release used by this merge |
| Execd | `v1.1.0` | Upstream release used by this merge |
| Ingress | `v1.0.10` | Unchanged component version |
| Server | `v0.2.3` | Server changes included in this merge |
| Task executor | `v0.2.0` | Unchanged component version |
| Image committer | `v0.1.1` | Unchanged component version |
| Node agent | `v0.1.0` | New component included in the chart |

The image references are:

```text
ghcr.io/jaluma/opensandbox/controller:v0.2.0
ghcr.io/jaluma/opensandbox/egress:v1.1.7
ghcr.io/jaluma/opensandbox/execd:v1.1.0
ghcr.io/jaluma/opensandbox/ingress:v1.0.10
ghcr.io/jaluma/opensandbox/server:v0.2.3
ghcr.io/jaluma/opensandbox/task-executor:v0.2.0
ghcr.io/jaluma/opensandbox/image-committer:v0.1.1
ghcr.io/jaluma/opensandbox/nodeagent:v0.1.0
```

## Helm Chart

The published umbrella chart is:

```text
Chart version: 0.2.5
App version:   0.2.3
```

The chart includes these dependencies:

- `opensandbox-controller` `0.2.1`
- `opensandbox-server` `0.2.3`
- `opensandbox-node-agent` `0.1.0`

Install it from the fork's Helm repository:

```bash
helm repo add opensandbox https://jaluma.github.io/OpenSandbox/helm
helm repo update
helm install opensandbox opensandbox/opensandbox \
  --version 0.2.5 \
  --namespace opensandbox-system \
  --create-namespace
```

The previous `0.2.4` chart remains in the repository index. The release
artifact and checksum are also available from the
[GitHub release](https://github.com/jaluma/OpenSandbox/releases/tag/helm/opensandbox/0.2.5).

## Fork Changes

This fork's release merge includes the upstream server, execd, egress, and
node-agent updates while retaining the upstream controller and ingress image
versions. It also includes:

- Docker `extra_hosts`, fleet-wide sandbox environment variables, and bind
  mounts.
- Server-side lifecycle validation and Docker lifecycle-hook rejection.
- Configurable egress sidecar readiness timeout.
- Deterministic Docker sandbox lookup with label-based fallback.
- The optional OpenSandbox node-agent chart and its airgap image entry.
- A regenerated umbrella `Chart.lock` and Helm publication workflow fixes.

For the complete upstream component release notes, see the
[OpenSandbox upstream releases](https://github.com/opensandbox-group/OpenSandbox/releases).
