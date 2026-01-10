# High-Availability Python Web App on Kubernetes (AWS)

## 👤 Author: M Zubair

## 🚀 Project Overview
This project showcases a production-ready deployment of a Python application using **Kubernetes**. I moved beyond simple Docker containers to build a self-healing, load-balanced infrastructure on an **AWS EC2** instance.

## 🛠️ Tech Stack
* **Infrastructure:** AWS EC2 (Ubuntu 24.04, t3.micro)
* **Orchestration:** Kubernetes (Minikube)
* **Containerization:** Docker
* **Language:** Python / Django

## 💡 Key Features Demonstrated
1.  **Self-Healing:** If a pod is deleted or crashes, Kubernetes automatically recreates it to maintain the desired state (2 replicas).
2.  **Load Balancing:** A `NodePort` service distributes traffic across multiple instances of the app.
3.  **Zero-Downtime Updates:** Implemented a rolling update strategy to move from `v1` to `v2` of the app.

## 📸 Proof of Concept
*(Note: I will upload my screenshots here)*
* **Cluster Status:** `kubectl get all`
* **Auto-Healing:** `kubectl delete pod` and watching the replacement.
* **Live App:** Running at `http://13.49.148.165:8080/demo/`
