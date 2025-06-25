# 🚀 GitOps Workflow using ArgoCD and Kubernetes

This project demonstrates a GitOps pipeline using **ArgoCD**, where Kubernetes deployment states are automatically synced from a **GitHub repository**. It uses **Minikube** as the local Kubernetes cluster and **Docker** for containerization.

## 📌 Objective

Implement GitOps by connecting a GitHub repo to ArgoCD so that any changes to Kubernetes manifests are automatically reflected in the cluster.

## 🛠 Tools Used

| Tool     | Description                                  |
|----------|----------------------------------------------|
| ArgoCD   | Declarative GitOps Continuous Delivery tool  |
| Kubernetes (Minikube) | Local container orchestration |
| GitHub   | Source repository for Kubernetes manifests   |
| Docker   | Container platform to build/test images      |

---

## 🧱 Project Structure

gitops-argocd-project/

├── app/

│ ├── deployment.yaml # Kubernetes Deployment

│ └── service.yaml # Kubernetes Service

├── argocd/

│ └── app.yaml # ArgoCD Application manifest

└── README.md # This documentation

## 🚀 How to Run This Project

### 1️⃣ Start Minikube

- Start a local Kubernetes cluster:

>> minikube start --memory=4096 --cpus=2

2️⃣ Install ArgoCD

>> kubectl create namespace argocd

>> kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

3️⃣ Expose ArgoCD UI
- Port forward the ArgoCD API server:
>>kubectl port-forward svc/argocd-server -n argocd 8080:443

Access ArgoCD UI at: https://localhost:8080

4️⃣ Login to ArgoCD
- Get the default admin password:

>> kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

Login via UI or CLI:

argocd login localhost:8080

5️⃣ Push Kubernetes Manifests to GitHub
Your app/ folder should contain:
-- deployment.yaml
-- service.yaml

- Push this folder to a public GitHub repo.

6️⃣ Create ArgoCD Application
argocd/app.yaml

- Apply the app.yaml:
>> kubectl apply -f argocd/app.yaml

7️⃣ ArgoCD Sync in Action
- Open the ArgoCD UI and see the application listed:
Status: Synced
Health: Healthy

Make a change in the GitHub repo (e.g., update replicas), commit and push, and watch ArgoCD auto-sync the update.

-----------------------------------------------------------------------------------------------------------------------------------------

**📸 Screenshots**
Include screenshots like:

- ArgoCD Dashboard
- App Status: Synced and Healthy
- Git commit → auto-deploy event

**💬 Notes**
GitOps enforces declarative, version-controlled infrastructure.

ArgoCD ensures continuous delivery with visibility and rollback capabilities.

**📄 Resume Line**
Implemented GitOps pipeline using ArgoCD and Kubernetes by auto-syncing application state from GitHub to Minikube.
