# Full Cycle 3.0 - Kubernetes Section

Welcome to the Kubernetes section of Full Cycle 3.0!

This guide will help you set up your environment with Docker and Kind, and teach you how to create a local Kubernetes cluster using Kind.

## Prerequisites

Before you begin, ensure you have the following installed:

- [Docker](https://docs.docker.com/get-docker/)
- [Kind (Kubernetes IN Docker)](https://kind.sigs.k8s.io/)

### Installing Docker

Follow the instructions for your operating system:

- **Windows/Mac:**  
  Download and install Docker Desktop from [here](https://www.docker.com/products/docker-desktop/).
- **Linux:**  
  Follow the official guide [here](https://docs.docker.com/engine/install/).

After installation, verify Docker is running:

```sh
docker --version
```

### Installing Kind

You can install Kind using the following command:

- **Linux/macOS:**

  ```sh
  curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-$(uname)-amd64
  chmod +x ./kind
  sudo mv ./kind /usr/local/bin/kind
  ```

- **Windows (using Chocolatey):**

  ```sh
  choco install kind
  ```

Verify Kind installation:

```sh
kind --version
```

## Creating a Kubernetes Cluster with Kind

To create a new Kubernetes cluster named `fullcycle`:

```sh
kind create cluster --name fullcycle
```

This will start a local Kubernetes cluster using Docker containers.

### Listing Clusters

To see all Kind clusters:

```sh
kind get clusters
```

### Deleting the Cluster

To delete the cluster when you're done:

```sh
kind delete cluster --name fullcycle
```

## Next Steps

You are now ready to start deploying applications to your local Kubernetes cluster!

For more information, visit the [Kind documentation](https://kind.sigs.k8s.io/) and [Kubernetes documentation](https://kubernetes.io/docs/).
