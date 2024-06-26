# Cluster Autoscaler

This flavor adds auto-scaling via [Cluster
Autoscaler](https://www.github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler#cluster-autoscaler).

## Specification

| Supported Control Plane | CNI    | Default OS   | Installs ClusterClass | IPv4 | IPv6 |
|-------------------------|--------|--------------|-----------------------|------|------|
| kubeadm, k3s, rke2      | Cilium | Ubuntu 22.04 | No                    | Yes  | Yes  |

## Prerequisites

[Quickstart](../getting-started.md) completed

## Usage

1. Set up autoscaling environment variables
    > We recommend using Cluster Autoscaler with the Kubernetes control plane
    > ... version for which it was meant.
    >
    > -- <cite>[Releases · kubernetes/autoscaler](https://www.github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler#releases)</cite>

    ```sh
    export CLUSTER_AUTOSCALER_VERSION=v1.29.0
    # Optional: If specified, these values must be explicitly quoted!
    export WORKER_MACHINE_MIN='"1"'
    export WORKER_MACHINE_MAX='"10"'
    ```

2. Generate cluster yaml

    ```sh
    clusterctl generate cluster test-cluster \
        --kubernetes-version v1.29.1 \
        --infrastructure linode-linode \
        --flavor <controlplane>-cluster-autoscaler > test-cluster.yaml
    ```

3. Apply cluster yaml

    ```sh
    kubectl apply -f test-cluster.yaml
    ```
