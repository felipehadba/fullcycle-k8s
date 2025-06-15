# Deployments, ReplicaSets, and Pods in Kubernetes

This guide will walk you through applying and monitoring the Kubernetes resources defined in this folder: **Pod**, **ReplicaSet**, and **Deployment**.  
You'll learn the concepts behind each, how to apply them, and what to expect in your terminal.

---

## Concepts Overview

- **Pod**: The smallest deployable unit in Kubernetes. A Pod encapsulates one or more containers.
- **ReplicaSet**: Ensures a specified number of identical Pods are running at all times.
- **Deployment**: Manages ReplicaSets and provides declarative updates for Pods and ReplicaSets.

---

## Building and Loading Your Docker Image into Kind

Before applying the manifests, you need to build the Docker image (`fc-goserver:1.0`) and load it into your Kind cluster - assuming your Kind cluster is named fullcycle.

```sh
cd ../Dockerfiles/go-server
docker build -t fc-goserver:1.0 .
kind load docker-image fc-goserver:1.0 --name fullcycle
```

---

## 1. Pod

### What is a Pod?
A Pod is a single instance of a running process in your cluster.

### Apply the Pod

```sh
kubectl apply -f k8s/pod.yaml
```

### Monitor the Pod:

```sh
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>
```

You should see your Pod running.

### Delete the Pod:
```sh
kubectl delete -f k8s/pod.yaml
```

The Pod will be removed.

---

## 2. ReplicaSet
### What is it?
A ReplicaSet ensures a specified number of Pod replicas are running.

Apply the ReplicaSet:

```sh
kubectl apply -f k8s/replicaset.yaml
```

### Monitor the ReplicaSet:

```sh
kubectl get replicasets
kubectl get pods
kubectl describe replicaset <replicaset-name>
```

You should see the ReplicaSet and its Pods running.

### Delete the ReplicaSet:

```sh
kubectl delete -f k8s/replicaset.yaml
```

The ReplicaSet and its Pods will be deleted.

---

## 3. Deployment
### What is it?
A Deployment manages ReplicaSets and provides declarative updates for Pods.

### Apply the Deployment:

```sh
kubectl apply -f k8s/deployment.yaml
```

### Monitor the Deployment:

```sh
kubectl get deployments
kubectl get replicasets
kubectl get pods
kubectl describe deployment <deployment-name>
```

You should see the Deployment, its ReplicaSet, and Pods running.

### Delete the Deployment:

```sh
kubectl delete -f k8s/deployment.yaml
```

The Deployment, its ReplicaSet, and Pods will be deleted.

---