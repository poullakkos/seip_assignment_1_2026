# 🚀 Cloud-Native Echo API – Kubernetes Deployment

This project demonstrates a complete cloud-native deployment pipeline using Docker, GitHub Container Registry (GHCR), and Kubernetes (Minikube). It follows DevOps best practices including CI/CD automation, configuration management, and container orchestration.

---

## 📦 Tech Stack

- Node.js (Express API)
- Docker
- GitHub Actions (CI/CD)
- GitHub Container Registry (GHCR)
- Kubernetes (Minikube)
- kubectl

---

## 📁 Repository Structure

```text
├── server.js
├── Dockerfile
├── package.json
├── k8s/
│   ├── configmap.yaml
│   ├── secret.yaml
│   ├── deployment.yaml
│   └── service.yaml
└── .github/workflows/
    └── ci-cd.yaml
```

---

## 📥 1. Clone the Repository

```bash
git clone https://github.com/poullakkos/seip_assignment_1_2026.git
cd seip_assignment_1_2026
```

---

## ⚙️ 2. Start Minikube Cluster

Ensure Minikube is installed and running:
```bash 
minikube start
```
Verify cluster is running:
```bash
kubectl get nodes
```
You should see a node in `Ready` state.

---

## 📦 3. Deploy Application to Kubernetes

Apply all Kubernetes manifests at once:
```bash
kubectl apply -f k8s/
```

This will create:

* ConfigMap (environment configuration)
* Secret (secure API key)
* Deployment (3 replicas of the app)
* Service (ClusterIP networking)

---

## 🔍 4. Verify Deployment

Check running pods:
```bash
kubectl get pods
```
Check services:
```bash
kubectl get services
```
Check full resource status:
```bash
kubectl get all
```

---

## 🌐 5. Access the Application (Port Forwarding)

Since the Service is of type `ClusterIP`, it is not publicly accessible.

Use port-forward to access it locally:
```bash
kubectl port-forward service/service 8080:80
```
Now open your browser:
[http://localhost:8080](http://localhost:8080)

---

## 📡 6. API Endpoints

### 🏠 Root Endpoint
`GET /`  
Returns welcome message and environment info.

### ❤️ Health Check
`GET /health`  
Used by Kubernetes liveness/readiness probes.

### 🔐 Secure Config Check
`GET /secure-config`  
Validates that Secret injection is working correctly.

---

## 🔐 Configuration Injection

This project uses:
* ConfigMap
    * WELCOME_MESSAGE
    * NODE_ENV
* Secret
    * API_SECRET_KEY (base64 encoded)

These values are injected into the container as environment variables.
