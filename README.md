# 737kubernetes - Kubernetes Deployment Project

This repository contains the code and configuration to deploy a simple Node.js application to a Kubernetes cluster using **Docker Desktop Kubernetes**.

---

## 🌊 Project Overview

We deployed a containerized Node.js Express application using:
- Docker for containerization
- Docker Hub for image hosting
- Kubernetes (via Docker Desktop) for orchestration

---

## ⚖️ Tools Used

- [Node.js](https://nodejs.org/en/)
- [Express.js](https://expressjs.com/)
- [Docker](https://www.docker.com/products/docker-desktop)
- [Docker Hub](https://hub.docker.com/)
- [Kubernetes](https://kubernetes.io/)
- [kubectl CLI](https://kubernetes.io/docs/reference/kubectl/)

---

## ✅ Steps to Deploy

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/737kubernetes.git
cd 737kubernetes
```

### 2. Build Docker Image
```bash
docker build -t abhishek2806/737kubernetes-image .
```

### 3. Push to Docker Hub
```bash
docker push abhishek2806/737kubernetes-image
```

### 4. Enable Kubernetes in Docker Desktop
- Open Docker Desktop > Settings > Kubernetes
- Check: **Enable Kubernetes**
- Click **Apply & Restart**

### 5. Apply Kubernetes Configs
```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### 6. Access the App
Check service details:
```bash
kubectl get service kube737-service
```

Visit:
```
http://localhost:30007
```

You should see:
> Hello from 737kubernetes Node.js app!

---

## 📂 Project Structure
```
737kubernetes/
├── Dockerfile
├── index.js
├── package.json
├── deployment.yaml
├── service.yaml
└── README.md
```

---

## 🔧 Kubernetes Files

### deployment.yaml
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: 737kubernetes-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: 737kubernetes
  template:
    metadata:
      labels:
        app: 737kubernetes
    spec:
      containers:
      - name: 737kubernetes
        image: abhishek2806/737kubernetes-image
        ports:
        - containerPort: 3000
```

### service.yaml
```yaml
apiVersion: v1
kind: Service
metadata:
  name: kube737-service
spec:
  type: NodePort
  selector:
    app: 737kubernetes
  ports:
    - protocol: TCP
      port: 3000
      targetPort: 3000
      nodePort: 30007
```

---

## 🔄 Cleanup
```bash
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml
```

---

## 📢 Contact
**Author**: Abhishek Srinivasan  
**DockerHub**: [abhishek2806](https://hub.docker.com/u/abhishek2806)

---

> Deployed using Docker Desktop Kubernetes for SIT737 Practical Task

