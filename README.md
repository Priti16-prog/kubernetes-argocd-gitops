# Kubernetes GitOps Voting Application

## Project Overview

This project demonstrates the deployment and management of a containerized Voting Application on an AWS EC2 instance using Kubernetes, Kind, Kubernetes Dashboard, and Argo CD.

The project follows a **GitOps approach**, where Kubernetes application manifests are maintained in GitHub and Argo CD continuously monitors the repository and synchronizes the desired state with the Kubernetes cluster.

## Architecture

```text
                         AWS EC2
                            |
                            v
                   Kind Kubernetes Cluster
                            |
              +-------------+-------------+
              |                           |
              v                           v
     Kubernetes Dashboard             Argo CD
                                          |
                                          v
                                  GitHub Repository
                                          |
                                          v
                              Kubernetes Manifests
                                          |
                                          v
                                  Voting Application
                                          |
                     +--------------------+--------------------+
                     |                    |                    |
                   Vote                 Worker               Result
                     |                    |                    |
                     +--------------------+--------------------+
                                          |
                                   Redis + PostgreSQL
```

## Technologies Used

* AWS EC2
* Ubuntu Linux
* Docker
* Kind (Kubernetes in Docker)
* Kubernetes
* kubectl
* Kubernetes Dashboard
* Argo CD
* Git
* GitHub
* PostgreSQL
* Redis

## Application Components

The Voting Application consists of the following components:

* **Vote Service** — Frontend interface for submitting votes
* **Result Service** — Displays voting results
* **Worker Service** — Processes votes between Redis and PostgreSQL
* **Redis** — Temporarily stores voting data
* **PostgreSQL** — Provides persistent storage for voting data

## GitOps Workflow

1. A Kubernetes cluster is created using Kind.
2. Kubernetes application manifests are maintained in the GitHub repository.
3. Argo CD monitors the GitHub repository for changes.
4. Argo CD automatically synchronizes Kubernetes resources with the desired state defined in Git.
5. **Auto-Sync** keeps the cluster aligned with the Git repository.
6. **Self-Heal** automatically corrects configuration drift.
7. **Prune** removes Kubernetes resources that are deleted from Git.

## Argo CD Configuration

The Argo CD application is configured with:

* **Automated Sync:** Enabled
* **Prune:** Enabled
* **Self-Heal:** Enabled
* **Target Namespace:** `default`
* **Manifest Path:** `k8s-specifications`

## Screenshots

### 1. Argo CD Application Tree

Argo CD monitors the GitHub repository and manages the desired state of the Voting Application. The application and its Kubernetes resources are displayed through the Argo CD application tree.

![Argo CD Application Tree](screenshots/argocd-application-tree.png)

### 2. Argo CD Application Network

The Argo CD network view provides a visual representation of the relationships between the deployed Kubernetes resources, services, deployments, and pods.

![Argo CD Application Network](screenshots/argocd-application-network.png)

### 3. Voting Application

The Voting Application is successfully deployed and accessible through the Kubernetes environment.

![Voting Application](screenshots/voting-application.png)

### 4. Argo CD Workload Status

The Argo CD workload view shows the status of the deployed application workloads and Kubernetes resources.

![Argo CD Workload Status](screenshots/argocd-workload-status.png)

### 5. AWS EC2 Inbound Rules

The EC2 security group inbound rules are configured to provide the required network access to the deployed Kubernetes environment.

![EC2 Inbound Rules](screenshots/ec2-inbound-rules.png)

## Repository Structure

```text
.
├── argocd/
│   └── application.yml
├── dashboard/
│   └── dashboard.yml
├── k8s-specifications/
│   ├── db-deployment.yaml
│   ├── db-service.yaml
│   ├── redis-deployment.yaml
│   ├── redis-service.yaml
│   ├── result-deployment.yaml
│   ├── result-service.yaml
│   ├── vote-deployment.yaml
│   ├── vote-service.yaml
│   └── worker-deployment.yaml
├── kind/
│   └── config.yml
├── scripts/
│   ├── install_kind.sh
│   └── install_kubectl.sh
├── screenshots/
│   ├── argocd-application-tree.png
│   ├── argocd-application-network.png
│   ├── voting-application.png
│   ├── argocd-workload-status.png
│   └── ec2-inbound-rules.png
└── README.md
```

## Project Outcome

Successfully deployed a multi-component Voting Application on Kubernetes running on AWS EC2 and implemented a **GitOps-based continuous delivery workflow using Argo CD**, including automated synchronization, self-healing, and resource pruning.

The project demonstrates practical experience with **AWS, Linux, Docker, Kubernetes, Kind, GitHub, and Argo CD-based GitOps deployment**.
