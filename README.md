# Kubernetes Ingress Portfolio Project

**Author:** Muhammad Zubair  
**Project:** High-Availability Python Web App on Kubernetes with Ingress  
**Purpose:** Demonstrates host/path-based routing using Kubernetes Ingress with ClusterIP services.

---

## Project Overview

This project showcases:

- Deploying a Python/Django web application on Kubernetes
- Exposing it using **ClusterIP services** (internal)
- Routing external traffic through **NGINX Ingress controller**
- Using **host and path-based routing**
- Single IP access for multiple services
- Cost-efficient architecture (no LoadBalancer per service)

---

## Files in the Repository

| File | Description |
|------|-------------|
| `deployment.yml` | Kubernetes Deployment manifest for Python/Django app |
| `service.yml` | ClusterIP Service manifest |
| `ingress.yml` | Ingress manifest with host/path routing |
| `Dockerfile` | Dockerfile for building the Python web app image |
| `requirements.txt` | Python dependencies |
| `README.md` | This file |
| `notes.md` | Step-by-step notes and explanations |

---

## Steps Performed

### 1. Created Kubernetes Deployment

```bash
kubectl apply -f deployment.yml
kubectl get pods
```

### 2. Exposed Deployment via ClusterIP Service
```bash
kubectl apply -f service.yml
kubectl get svc
```
### 3. Installed NGINX Ingress Controller
```bash
minikube addons enable ingress
kubectl get pods -n ingress-nginx
```
### 4. Created Ingress Resource
```bash
kubectl apply -f ingress.yml
kubectl get ingress
```
### 5. Configured /etc/hosts for local testing
```bash
sudo vi /etc/hosts
```
### 6. Tested Access
```bash
curl http://app.example.com/demo/
```


