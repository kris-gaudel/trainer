# Kubeflow Trainer Helm Chart

This Helm chart deploys Kubeflow Trainer on Kubernetes.

## Prerequisites

- kubectl configured to communicate with your cluster

## Installation

### Method 1: Direct OCI Installation

```bash
helm install kubeflow-trainer oci://ghcr.io/kubeflow/helm-charts/kubeflow-trainer \
    --version 2.0.0 \
    --namespace kubeflow-system \
    --create-namespace
```

### Method 2: Using Helm Repository

```bash
# Add the Helm repository
helm repo add kubeflow-trainer https://kubeflow.github.io/trainer

# Update the repository
helm repo update

# Install the chart
helm install kubeflow-trainer kubeflow-trainer/kubeflow-trainer \
    --version 2.0.0 \
    --namespace kubeflow-system \
    --create-namespace
```

## Configuration

The following table lists the configurable parameters of the kubeflow-trainer chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `nameOverride` | String to partially override release name | `""` |
| `fullnameOverride` | String to fully override release name | `""` |
| `jobset.install` | Whether to install jobset as a dependency | `true` |
| `image.registry` | Image registry | `"docker.io"` |
| `image.repository` | Image repository | `"kubeflow/trainer-controller-manager"` |
| `image.tag` | Image tag | Chart version |
| `image.pullPolicy` | Image pull policy | `"IfNotPresent"` |
| `manager.replicas` | Number of replicas of manager | `1` |
| `manager.resources` | Pod resource requests and limits | `{}` |

For more configuration options, please refer to the [values.yaml](values.yaml) file.

## Uninstalling the Chart

To uninstall/delete the deployment:

```bash
helm uninstall kubeflow-trainer -n kubeflow-system
```

## Troubleshooting

If you encounter any issues during installation:

1. Check the pod status:
   ```bash
   kubectl get pods -n kubeflow-system
   ```

2. Check the pod logs:
   ```bash
   kubectl logs -n kubeflow-system -l app.kubernetes.io/name=kubeflow-trainer
   ```

3. Verify the Helm release:
   ```bash
   helm list -n kubeflow-system
   ```

## Contributing

Please refer to the [contributing guide](../../CONTRIBUTING.md) for details on our code of conduct and the process for submitting pull requests.

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](../../LICENSE) file for details.
