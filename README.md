# CST8918 - DevOps: Infrastructure as Code
## Lab A01 - Weather App Submission
**Student:** Divyang Lodariya  
**Course:** 26S_CST8918_300  
**Date:** May 18, 2026

---

## Overview

This lab demonstrates containerizing a Node.js (Remix) weather application and deploying it to a local Kubernetes cluster using Docker Desktop.

---

## Part 1 - Web Application

The weather app was cloned, dependencies installed, and run locally using the OpenWeather API.

- Framework: Remix (React meta-framework)
- API: OpenWeather Current Weather API
- Local dev server running at: `http://localhost:3000`

### App Running Locally (localhost:3000)
![App running at localhost:3000] <img width="1917" height="1025" alt="localhost 3000" src="https://github.com/user-attachments/assets/9c135e92-50a9-45af-ba0f-f74dd24057ff" />


---

## Part 2 - Docker Container

The app was containerized using the provided Dockerfile and tested locally before pushing to Docker Hub.

- Docker image: `divyang25/cst8918-a01-weather-app`
- Container tested at: `http://localhost:8080`

### App Running in Docker Container (localhost:8080)
![App running in Docker container] <img width="1917" height="967" alt="localhost 8080" src="https://github.com/user-attachments/assets/1b21e043-023d-4d7f-8b6e-77f50d20eaf0" />


---

## Part 3 - Kubernetes Deployment

The containerized app was deployed to a local Kubernetes cluster running on Docker Desktop.

### Kubernetes Resources Created

| Resource | Name | Namespace |
|---|---|---|
| Namespace | cst8918 | - |
| Deployment | weather-app-deployment | cst8918 |
| Service | weather-app-service (LoadBalancer) | cst8918 |
| Secret | weather (API key) | cst8918 |

### Kubernetes Manifest Files

- `k8s/a01_namespace.yaml` - Namespace definition
- `k8s/a01_deployment.yaml` - Deployment with 2 replicas
- `k8s/a01_service.yaml` - LoadBalancer service on port 80

### App Running via Kubernetes (localhost:80)
![App running via Kubernetes] <img width="1917" height="1020" alt="localhost running" src="https://github.com/user-attachments/assets/482f3e95-46ab-4bea-8301-ee964f6e711a" />


### Kubernetes Cluster Status
![kubectl get namespaces, services, pods] <img width="1512" height="805" alt="image" src="https://github.com/user-attachments/assets/e6d856fa-9e8f-4893-a37c-84f5963839ea" />


---

## Kubernetes Commands Used

```bash
# Apply namespace
kubectl apply -f ./k8s/a01_namespace.yaml

# Create API key secret
kubectl create secret generic weather --from-literal='api-key=<redacted>' -n cst8918

# Deploy the application
kubectl apply -f ./k8s/a01_deployment.yaml -n cst8918

# Create the load balancer service
kubectl apply -f ./k8s/a01_service.yaml -n cst8918

# Verify deployment
kubectl get namespaces
kubectl get services -n cst8918
kubectl get pods -n cst8918
```

---

## Verification Output

```
NAME                                   READY   STATUS    RESTARTS   AGE
weather-app-deployment-6797dc657c-hvrkh   1/1     Running   0          9m47s
weather-app-deployment-6797dc657c-lckwx   1/1     Running   0          9m47s
```

Both pods running successfully with 2 replicas as configured.

---

## Docker Hub

Image published at: `docker.io/divyang25/cst8918-a01-weather-app`
