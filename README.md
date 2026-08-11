# Kubernetes GitOps Voting Application

## Project Overview

This project demonstrates the deployment and management of a containerized Voting Application on an AWS EC2 instance using Kubernetes, Kind, Kubernetes Dashboard, and Argo CD.

The project follows a GitOps approach where Kubernetes application manifests are stored in GitHub and Argo CD continuously monitors the repository and synchronizes the desired state with the Kubernetes cluster.

## Architecture

AWS EC2
   |
   v
Kind Kubernetes Cluster
   |
   +----------------------+
   |                      |
   v                      v
Kubernetes Dashboard    Argo CD
                           |
                           v
                    GitHub Repository
                           |
                           v
                  Kubernetes Manifests
                           |
                           v
                 Voting Application
                 |       |       |
                Vote   Worker  Result
                         |
                    Redis + PostgreSQL

## Technologies Used

- AWS EC2
- Ubuntu Linux
- Docker
- Kind (Kubernetes in Docker)
- Kubernetes
- kubectl
- Kubernetes Dashboard
- Argo CD
- Git
- GitHub
- PostgreSQL
- Redis

## Application Components

The Voting Application consists of:

- Vote service - Frontend for submitting votes
- Result service - Displays voting results
- Worker service - Processes votes
- Redis - Stores votes temporarily
- PostgreSQL - Stores persistent voting data

## GitOps Workflow

1. Kubernetes cluster is created using Kind.
2. Voting application Kubernetes manifests are stored in GitHub.
3. Argo CD monitors the GitHub repository.
4. Argo CD automatically synchronizes Kubernetes resources.
5. Auto-Sync keeps the cluster aligned with the Git repository.
6. Self-Heal automatically corrects configuration drift.
7. Prune removes resources that are deleted from Git.
   
## Argo CD Configuration

The Argo CD application is configured with:

- Automated Sync: Enabled
- Prune: Enabled
- Self-Heal: Enabled
- Target Namespace: default
- Manifest Path: k8s-specifications

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
└── README.md
## Project Outcome

Successfully deployed a multi-component Voting Application on Kubernetes running on AWS EC2 and implemented GitOps-based continuous delivery using Argo CD with automated synchronization, self-healing, and resource pruning.
