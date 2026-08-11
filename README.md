# OCI Kubernetes Deployment Architecture

## Overview

The repository shows a simple application deployment flow using Oracle Kubernetes Engine, Kubernetes Deployment, Service, Ingress, and OCI Load Balancer.
My focus was to explain how traffic moves from an external user to the OCI Load Balancer, then to the Ingress Controller, Kubernetes Service, and finally to the application pods running on worker nodes.
This contribution demonstrates my understanding of how OKE and OCI networking components work together to support application deployment. No client-confidential, proprietary, or project-specific information is included.

---

## Why I Created This

Kubernetes can look complex when the deployment, service, ingress, and load balancer are reviewed separately.

I created this repository to break the flow into simple sections. The goal is to understand how a basic web application can be deployed on OKE and how traffic reaches the application through Kubernetes and OCI networking components.

---

## Product Used

Oracle Kubernetes Engine on Oracle Cloud Infrastructure

---

## Simple Architecture Flow

```mermaid
flowchart TD
    A[External User] --> B[OCI Load Balancer]
    B --> C[Ingress Controller]
    C --> D[Kubernetes Service - ClusterIP]
    D --> E[OKE Worker Node 1 - NGINX Pod]
    D --> F[OKE Worker Node 2 - NGINX Pod]
```

This is a simple product usage example. In an actual implementation, the design may change based on security, network design, DNS, certificates, scaling, and application requirements.

---

## Components Covered

This repository covers the following components:

- Oracle Kubernetes Engine
- OCI Load Balancer
- Kubernetes Deployment
- Kubernetes Service
- Kubernetes Ingress
- NGINX container image
- Basic external traffic flow to application pods

---

## Kubernetes Resources Included

### Deployment

The deployment file creates two replicas of a simple NGINX web application pod.

File:

```text
kubernetes-manifests/deployment.yaml
```

### Service

The service file exposes the application inside the Kubernetes cluster using ClusterIP.

File:

```text
kubernetes-manifests/service.yaml
```

### Ingress

The ingress file defines how external HTTP traffic should be routed to the Kubernetes service.

File:

```text
kubernetes-manifests/ingress.yaml
```

The host value used in this repository is only a sample value.

---

## Deployment Commands

Apply the deployment:

```bash
kubectl apply -f kubernetes-manifests/deployment.yaml
```

Apply the service:

```bash
kubectl apply -f kubernetes-manifests/service.yaml
```

Apply the ingress:

```bash
kubectl apply -f kubernetes-manifests/ingress.yaml
```

---

## Verification Commands

Check the pods:

```bash
kubectl get pods
```

Check the service:

```bash
kubectl get svc
```

Check the ingress:

```bash
kubectl get ingress
```

---

## What I Understood

The key point from this exercise is that OKE application deployment should not be viewed only as creating pods.

A working deployment needs multiple layers to work together. The Deployment keeps the application pods running. The Service provides internal access to the pods. The Ingress defines the external routing rule. The OCI Load Balancer helps route traffic from outside the cluster.

This helped me understand the basic relationship between OKE, Kubernetes resources, and OCI load balancing.

---

## Confidentiality Note

All examples in this repository are based on my own product usage and documentation. No client-confidential, proprietary, or project-specific information is included.
