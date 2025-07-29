# ArgoCD Tutorial

<br />

## Table of Contents
- [What is GitOps](#what-is-gitops)
- [Install ArgoCD](#install-argocd)
- [ArgoCD Architecture](#argocd-architecture)
- [Deployment Modes](#deployment-modes)

<br />
<br />

## What is GitOps

![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1753703925/432b611d-14e6-4dd1-a6f5-e85729648ded.png)

- `GitOps` is the idea of storing your entire system’s desired state (infrastructure + applications) in `Git`, and using automation tools / we can say `GitOps Controllers` (like ArgoCD or Flux) to continuously sync the actual system to match that desired state
- `GitOps` is the modern way of implementing CD
- Use `Git` as a `single source of truth` to deliver applications and infrastructures
- Track the infrastructures and applications deliveries

### Without GitOps
- `If our source code has a machanism of tracking so don't we have a tracking machanisam for deployments and infrasturctures ?`
- `We have proper CI with GIT integrated approach but why don't we have proper GIT integrated approach for CD ?`

### Core Concepts of GitOps

![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1753704805/ac964152-7174-4cb3-b6f8-26635295cead.png)

| Concept                       | Description                                                                                               |
| ----------------------------- | --------------------------------------------------------------------------------------------------------- |
| **Git as Source of Truth**    | All infrastructure & deployment configs are stored in Git repositories (e.g., YAML files for Kubernetes). |
| **Declarative Configuration** | You define what the system should look like, not how to get there (e.g., Kubernetes manifests).           |
| **Automation**                | A GitOps tool watches the Git repo and automatically applies changes to the cluster.                      |
| **Continuous Reconciliation** | The tool continuously checks for drift between Git and the live environment, and brings it back in sync.  |

### Benefits of GitOps
`Auditability`: Git history shows who changed what and when
`Rollback`: Revert to a previous state by reverting a Git commit
`Consistency`: Environments can be replicated using the same Git repo
`Security`: Reduce the need for direct cluster access (changes go through Git PRs)

### GitOps Workflow

![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1753706612/a8e7aa59-433b-4396-a816-a72a58bd611a.png)

<br />
<br />

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

![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1753695564/argocd_architecture_lgxeog.webp)
![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1753720373/61e01025-853a-4af0-a89d-e7e626ffbc0e.png)
![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1753720537/785c2581-8aa4-40f6-8d5d-4041409fde5b.png)

## Deployment Modes

- Read about the  [Hub-Spoke Model](https://medium.com/@biekrogodbless/hub-and-spoke-architecture-project-with-argocd-an-elastic-kubernetes-project-by-godbless-biekro-a3512e1e5701)
- Read about [deployment models](https://codefresh.io/learn/argo-cd/a-comprehensive-overview-of-argo-cd-architectures-2025/)
