# 🚀 Project 2: Kubernetes Deployment

Deploying the Docker image from Project 1 to a Kubernetes cluster with production-grade practices.

https://github.com/gitbsns/k8s-deployment/blob/main/screenshots/cloudflaredash.png
https://github.com/gitbsns/k8s-deployment/blob/main/screenshots/k8sscaled.png
https://github.com/gitbsns/k8s-deployment/blob/main/screenshots/kube.png
https://github.com/gitbsns/k8s-deployment/blob/main/screenshots/kubeapp.png
https://github.com/gitbsns/k8s-deployment/blob/main/screenshots/kubedeployment.png
https://github.com/gitbsns/k8s-deployment/blob/main/screenshots/kubepod.png
https://github.com/gitbsns/k8s-deployment/blob/main/screenshots/kubeurl.png

---

## 📌 Project Overview

This project takes the containerized Node.js application from **Project 1** and deploys it to a Kubernetes cluster. It demonstrates core Kubernetes concepts including Deployments, Services, ConfigMaps, Secrets, health probes, resource limits, and self-healing.

**What this project proves:**
- Declarative infrastructure with YAML manifests
- Multi-replica deployments with load balancing
- Configuration & secret management
- Health checks for reliability
- Self-healing and rolling updates

---

## 🏗️ Architecture

## 🏗️ Architecture

```mermaid
flowchart TD
    User([User / Browser]) -->|HTTP| Service[myapp-service NodePort 30007]
    Service -->|Load Balance| Pod1[Pod 1 abhdoc/project1:latest]
    Service -->|Load Balance| Pod2[Pod 2 abhdoc/project1:latest]
    CM[ConfigMap myapp-config] -.->|Env Vars| Pod1
    CM -.->|Env Vars| Pod2
    SEC[Secret myapp-secret] -.->|Secrets| Pod1
    SEC -.->|Secrets| Pod2
    Deploy[Deployment myapp-deployment Replicas 2] -->|Manages| Pod1
    Deploy -->|Manages| Pod2

Component Overview
Component	Type	Purpose
Deployment	myapp-deployment	Manages 2 replicas of the app
Pods	2x myapp	Running containers
Service	myapp-service (NodePort)	Exposes app on port 30007
ConfigMap	myapp-config	Non-sensitive env vars
Secret	myapp-secret	Sensitive data (base64)
🛠️ Tech Stack
Category	Tools
Orchestration	Kubernetes (Minikube)
CLI	kubectl
Container Runtime	Docker
Configuration	YAML
Application	Node.js / Express
Image Registry	Docker Hub
📁 Project Structure
text
project2/
├── k8s-manifests/
│   ├── configmap.yaml      # Environment variables
│   ├── secret.yaml         # Sensitive data (base64)
│   ├── deployment.yaml     # Pods + ReplicaSet (2 replicas)
│   └── service.yaml        # NodePort service
└── README.md
🚀 Deployment Steps
Prerequisites
Minikube installed and running

kubectl configured

Docker image abhdoc/project1:latest available on Docker Hub

Minimum 2 CPUs and 2GB RAM

1. Start Minikube
bash
minikube start --driver=docker --cpus=2 --memory=1800
2. Apply Manifests
bash
cd k8s-manifests
kubectl apply -f .
Expected output:

text
configmap/myapp-config created
secret/myapp-secret created
deployment.apps/myapp-deployment created
service/myapp-service created
3. Verify Deployment
bash
kubectl get pods
kubectl get svc
kubectl get deployment
kubectl get all
4. Access the Application
bash
minikube service myapp-service --url
Open the URL in your browser. Test these endpoints:

Endpoint	Purpose
/	App greeting
/info	ConfigMap/Secret verification
/health	Health check
🎯 Key Kubernetes Concepts Demonstrated
Concept	Where Used
Deployment	2 replicas of the app
Service (NodePort)	Exposing app on port 30007
ConfigMap	APP_ENV, APP_NAME, LOG_LEVEL
Secret	SESSION_SECRET (base64)
Liveness Probe	Auto-restart unhealthy pods
Readiness Probe	No traffic until pod ready
Resource Limits	CPU/RAM requests and limits
Labels & Selectors	Service → Pod discovery
ReplicaSet	Ensures desired pod count
