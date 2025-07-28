# ArgoCD Tutorial

## Table of Contents
- [What is GitOps](#what-is-gitops)
- [Install ArgoCD](#install-argocd)
- [ArgoCD Architecture](#argocd-architecture)

## What is GitOps

## Install ArgoCD
- ArgoCD is running on Minikube cluster
- We need to start `Minikube` cluster
```cmd
minikube start
```
- Create a Namespace for Argo CD
```cmd
kubectl create namespace argocd
```
- Install Argo CD
```cmd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
- Access Argo CD UI
```cmd
kubectl port-forward svc/argocd-server -n argocd 8000:443
kubectl port-forward svc/argocd-server -n argocd 8000:443
```
- Get the Initial Admin Password
```cmd
# Use Powershell for windows

# Step 1: Get the base64-encoded password
$base64Password = kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}"

# Step 2: Decode it
[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($base64Password))

# Username: admin
# Password: Output from the command above
```

## ArgoCD Architecture