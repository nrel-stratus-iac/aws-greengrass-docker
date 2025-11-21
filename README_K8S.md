# AWS IoT Greengrass v2 Deployment

Deploy AWS IoT Greengrass v2 to your Kubernetes cluster with ease.

## Prerequisites

Before you begin, ensure you have:
- A running Kubernetes cluster
- `kubectl` configured and connected to your cluster
- `helm` v3+ installed
- AWS IoT Greengrass v2 credentials ready

## Quick Start

### Step 1: Create Secret

First, apply the Greengrass v2 environment secret to your cluster:

```bash
kubectl apply -f secret-greengrass-v2-env.yaml -n greengrass
```

This creates the necessary credentials and configuration in the `greengrass` namespace.

### Step 2: Deploy the Helm Chart

Package and deploy the Greengrass v2 Helm chart:

```bash
# Package the Helm chart
helm package helm-chart

# Deploy to Kubernetes
helm upgrade --install greengrass-v2 greengrass-v2-*.tgz \
  -n greengrass \
  -f values-provision.yaml
```

The `--install` flag ensures the chart is installed if it doesn't exist, or upgraded if it does.

## Verify Deployment

Check that your Greengrass pods are running:

```bash
kubectl get pods -n greengrass
```

View the logs:

```bash
kubectl logs -f deployment/greengrass-v2 -n greengrass
```

## Configuration

Customize your deployment by editing `values-provision.yaml`.