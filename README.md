# ALTCHA Sentinel Helm Chart

## Overview

This Helm chart deploys [ALTCHA Sentinel](https://altcha.org/) on a Kubernetes cluster.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+
- PV provisioner support in the underlying infrastructure

## Installation

### Add the Helm repository

```bash
helm repo add altcha-org https://altcha-org.github.io/helm-charts
```

### Install the chart

```bash
helm install altcha-sentinel altcha-org/sentinel
```

## Configuration

The following table lists the configurable parameters of the ALTCHA Sentinel chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `replicaCount` | Number of replicas | `1` |
| `image.repository` | Container image repository | `ghcr.io/altcha-org/sentinel` |
| `image.tag` | Container image tag | `""` |
| `image.pullPolicy` | Container image pull policy | `IfNotPresent` |
| `service.type` | Kubernetes Service type | `LoadBalancer` |
| `service.port` | Service external port | `80` |
| `service.targetPort` | Container port | `8080` |
| `persistence.enabled` | Enable persistence | `true` |
| `persistence.accessMode` | PVC access mode | `ReadWriteOnce` |
| `persistence.size` | PVC size | `10Gi` |
| `persistence.storageClass` | PVC storage class | `""` (uses default) |
| `persistence.mountPath` | Mount path for volume | `/data` |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example:

```bash
helm install altcha-sentinel \
  --set persistence.size=20Gi \
  altcha-org/sentinel
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example:

```bash
helm install altcha-sentinel -f values.yaml altcha-org/sentinel
```

## Persistence

The ALTCHA Sentinel chart persists data to a Kubernetes PersistentVolume by default. The persistent volume claim is created with the following settings by default:
- 10Gi storage size
- ReadWriteOnce access mode
- Mounted at `/data` in the container

## Upgrading

To upgrade your release with new configuration:

```bash
helm upgrade altcha-sentinel altcha-org/sentinel -f values.yaml
```

## Uninstalling

To uninstall/delete the `altcha-sentinel` deployment:

```bash
helm delete altcha-sentinel
```

The command removes all the Kubernetes components associated with the chart and deletes the release.