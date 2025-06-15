# Kubernetes Services: ClusterIP, NodePort, and LoadBalancer

This guide explains the three main types of Kubernetes Services and how to apply, monitor, delete, and access each one from your local machine.

---

## Concepts Overview

- **Service**: An abstraction that exposes your application running on a set of Pods as a network service. Services enable communication within the cluster and, depending on the type, can also expose your app outside the cluster.

  - **ClusterIP**: Exposes the service on a cluster-internal IP. Accessible only within the cluster.
  - **NodePort**: Exposes the service on each Node’s IP at a static port. Accessible from outside the cluster using `<NodeIP>:<NodePort>`.
  - **LoadBalancer**: Exposes the service externally using a cloud provider’s load balancer. In local environments like Kind, you can simulate this using port forwarding or tools like MetalLB.


---

## 1. ClusterIP

**Description:**
- Exposes the service on a cluster-internal IP. Only accessible within the cluster.

**Apply:**
```sh
kubectl apply -f k8s/service-clusterip.yaml
```
**Monitor:**
```sh
kubectl get services
kubectl describe service goserver-clusterip
```
**Access from localhost:**
You can use port-forwarding to access the ClusterIP service from your machine:
```sh
kubectl port-forward service/goserver-clusterip 8080:80
```
Then open [http://localhost:8080](http://localhost:8080) in your browser.

**Delete:**
```sh
kubectl delete -f k8s/service-clusterip.yaml
```

---

## 2. NodePort

**Description:**
- Exposes the service on each Node's IP at a static port (the NodePort). Accessible from outside the cluster using `<NodeIP>:<NodePort>`.

**Apply:**
```sh
kubectl apply -f k8s/service-nodeport.yaml
```
**Monitor:**
```sh
kubectl get services
kubectl describe service goserver-nodeport
```
**Access from localhost:**
If using Kind, you can access the service via the NodePort on localhost. For example, if your NodePort is `30080`:
```sh
curl http://localhost:30080
```
Or open [http://localhost:30080](http://localhost:30080) in your browser.

**Delete:**
```sh
kubectl delete -f k8s/service-nodeport.yaml
```

---

## 3. LoadBalancer

**Description:**
- Exposes the service externally using a cloud provider's load balancer. In local environments (like Kind), this may require an additional tool (e.g., MetalLB) to work.

---

## Summary Table

| Service Type  | File                   | Access Scope         | Access Command/URL                |
|---------------|------------------------|----------------------|-----------------------------------|
| ClusterIP     | service-clusterip.yaml | Internal only        | `http://localhost:8080`           |
| NodePort      | service-nodeport.yaml  | External via NodeIP  | `http://localhost:30080`          |
| LoadBalancer  | N/A                    | External via LB      | External IP or port-forward       |
