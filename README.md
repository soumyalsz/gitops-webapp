## GitOps Automated Web App Pipeline using ArgoCD

This is a project I built to show automated deployments. Instead of manually updating servers or messing with cluster configs directly, the entire infrastructure lifecycle is managed entirely through Git. A single git push triggers the entire update process automatically.

## Tech Stack
1. App: Custom dark-mode developer dashboard (index.html)
2. Containerization: Docker (hosted on Docker Hub)
3. Orchestration: Kubernetes (running locally via Minikube)
4. GitOps Controller: ArgoCD

## Workflow
1. Code modifications and Kubernetes manifests (Deployment, Service, ConfigMap) are committed and pushed to this GitHub repository.
2. ArgoCD runs inside the Minikube cluster and monitors the /k8s path in this repository.
3. When a new commit is detected, ArgoCD automatically reconciles the cluster state with the repository state.
4. New pods are spun up with the updated v2 image, health checked, and old pods are terminated with zero downtime.
5. Developer metadata and cluster settings are dynamically injected using a Kubernetes ConfigMap to keep the application configuration separate from the code.


### ArgoCD Visual Tree
Active cluster state showing fully synchronized deployment primitives:
![ArgoCD Sync Status](./screenshots/argocd-sync.png)

### Live Web Application
The running web interface accessed through the Minikube service bridge:
![Live Web App](./screenshots/webapp-live.png)

## Environment Info
* Dev: soumyalsz
* Context: Local-Minikube-Node