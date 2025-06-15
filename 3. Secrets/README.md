# Kubernetes ConfigMap, Secret, and Deployment Guide

This guide explains how to use ConfigMap and Secret in Kubernetes, how to build and load the Go server image (version 2.0), and how to apply, monitor, and delete the manifests in the `k8s/` directory.

---

## 1. Building and Loading the Docker Image

Before applying the Kubernetes manifests, build the Docker image (`fc-goserver:2.0`) and load it into your Kind cluster (named `fullcycle`):

```sh
cd ../../Dockerfiles/go-server/v.2.0
docker build -t fc-goserver:2.0 .
kind load docker-image fc-goserver:2.0 --name fullcycle
```

---

## 2. ConfigMap and Secret Overview

- **ConfigMap**: Stores non-confidential configuration data in key-value pairs. See [`k8s/configmap.yaml`](k8s/configmap.yaml).
- **Secret**: Stores sensitive data (like passwords or tokens) in base64 encoded format. See [`k8s/secret.yaml`](k8s/secret.yaml).

Both can be mounted as environment variables or files in your pods.

---

## 3. Deployments

There are two deployment options:

- [`deployment-env.yaml`](k8s/deployment-env.yaml): Sets environment variables directly in the manifest.
- [`deployment-configmap.yaml`](k8s/deployment-configmap.yaml): Reads environment variables from the ConfigMap and Secret.

> **Note:** Both deployment files use the same `app` and deployment name (`goserver`). Because of this, you cannot deploy both at the same time. If you try, one will overwrite the other. Choose only one deployment file to apply at a time, depending on your configuration needs.

---

## 4. Applying the Kubernetes Manifests

Apply all resources in the `k8s/` directory:

```sh
kubectl apply -f k8s/
```

Or, to use the deployment that reads from ConfigMap and Secret:

```sh
kubectl apply -f k8s/configmap.yaml
kubectl apply -f k8s/secret.yaml
kubectl apply -f k8s/deployment-configmap.yaml
kubectl apply -f k8s/service-clusterip.yaml
```

---

## 5. Monitoring Resources

Check the status of your resources:

```sh
kubectl get deployments
kubectl get pods
kubectl get configmaps
kubectl get secrets
```

Describe resources for more details:

```sh
kubectl describe deployment goserver
kubectl describe configmap goserver-env
kubectl describe secret goserver-secret
```

Check pod logs:

```sh
kubectl logs <pod-name>
```

---

## 6. Accessing the Application

To access the application from your local machine, use port-forwarding:

```sh
kubectl port-forward svc/goserver-clusterip 8080:80
```

Then, open your browser or use `curl` to test the endpoints:

- http://localhost:8080/
- http://localhost:8080/secret
- http://localhost:8080/configmap

---

## 7. Deleting the Resources

To delete all resources created from the manifests:

```sh
kubectl delete -f k8s/
```

---

## 8. Notes

- The Go server in version 2.0 reads environment variables and can also read a file (see `/configmap` endpoint in the code).
- Ensure your deployment manifest uses the `fc-goserver:2.0` image and mounts the ConfigMap or Secret as needed.

