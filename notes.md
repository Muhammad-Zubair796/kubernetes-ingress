
---

````markdown
# Kubernetes Ingress Project - Detailed Notes

**Author:** Muhammad Zubair  
**Project:** Python/Django Web App on Kubernetes with Ingress  

---

## 1. Project Setup

- Created project folder:

```bash
mkdir ~/my-portfolio-project
cd ~/my-portfolio-project
````

* Added project files:

```
Dockerfile
requirements.txt
deployment.yml
service.yml
ingress.yml
README.md
```

---

## 2. Kubernetes Deployment

* Applied the Deployment:

```bash
kubectl apply -f deployment.yml
```

* Verified Pods:

```bash
kubectl get pods
```

**Output:**

```
zubi-python-deployment-7bd4cbb84-5rkpg   1/1 Running
zubi-python-deployment-7bd4cbb84-mflm4   1/1 Running
```

> Two replicas of Django app running successfully.

---

## 3. Exposing Deployment via Service

* Applied ClusterIP Service:

```bash
kubectl apply -f service.yml
kubectl get svc
```

**Output:**

```
NAME                  TYPE        CLUSTER-IP      PORT(S)
zubi-python-service   ClusterIP   10.99.233.195   80/TCP
```

> ClusterIP service exposes the app internally. No LoadBalancer IP required because Ingress handles external traffic.

---

## 4. Installing NGINX Ingress Controller

* Enabled Ingress addon in Minikube:

```bash
minikube addons enable ingress
```

* Checked Ingress pods:

```bash
kubectl get pods -n ingress-nginx
```

**Output:**

```
ingress-nginx-controller-9cc49f96f-c7jf2   1/1 Running
ingress-nginx-admission-create-9qcr2       0/1 Completed
ingress-nginx-admission-patch-sbwhm        0/1 Completed
```

---

## 5. Creating Ingress Resource

* Applied Ingress manifest:

```bash
kubectl apply -f ingress.yml
kubectl get ingress
```

**Output:**

```
NAME             CLASS   HOSTS             ADDRESS        PORTS
simple-ingress   nginx   app.example.com   192.168.49.2   80
```

* Host: `app.example.com`
* Path: `/demo` → routed to `zubi-python-service`

---

## 6. Editing `/etc/hosts` for local testing

* Mapped hostname to Minikube IP:

```bash
sudo vi /etc/hosts
```

Added:

```
192.168.49.2  app.example.com
```

* Verified ping:

```bash
ping app.example.com
```

**Output:**

```
PING app.example.com (192.168.49.2): 56 data bytes
64 bytes from 192.168.49.2: icmp_seq=1 ttl=64 time=0.054 ms
```

---

## 7. Testing the App

* Using curl:

```bash
curl http://app.example.com/demo/
```

* Browser testing:

```
http://app.example.com/demo/
```

> Note: `curl` worked on Git Bash; Chrome may require `/etc/hosts` mapping or port forwarding.

* 404 observed on `/` → Django URLconf only has `/demo` and `/admin`.

---

## 8. GitHub Version Control

* Initialized Git and added remote:

```bash
git init
git remote add origin https://github.com/Muhammad-Zubair796/kubernetes-ingress.git
```

* Added files and committed:

```bash
git add deployment.yml service.yml ingress.yml Dockerfile requirements.txt
git commit -m "Add initial Kubernetes manifests and Dockerfile"
```

* Pulled remote commits and rebased:

```bash
git pull origin main --rebase
```

* Pushed to GitHub:

```bash
git push -u origin main
```

> Repository now contains all manifests and Dockerfile for portfolio.

---

## 9. Learned Concepts

1. **ClusterIP vs LoadBalancer vs NodePort**

   * ClusterIP → internal only
   * LoadBalancer → public IP per service
   * NodePort → exposes service on node port

2. **Ingress Purpose**

   * Single IP for all services
   * Host/path-based routing
   * Cost-efficient external access

3. **NGINX Ingress Controller**

   * Watches Ingress rules
   * Routes external HTTP requests to correct ClusterIP services

4. **Debugging Techniques**

   * `/etc/hosts` for local DNS
   * `curl` vs browser testing
   * 404 errors vs cluster misconfigurations

---

## 10. Next Steps / Improvements

* Add multiple paths (`/admin`, `/products`) for different services
* Configure TLS certificates for HTTPS traffic
* Deploy to a cloud Kubernetes cluster for real external access

---

**Conclusion:**

This notes file documents **all steps, commands, and outputs** for deploying a Python/Django app on Kubernetes using ClusterIP services and Ingress.

```
