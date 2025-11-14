# Kubeflow Deployment Repository

This repository contains the manifests and configuration for deploying/upgrading **Kubeflow** on the Kubernetes cluster. The deployment is fully managed using **ArgoCD**, enabling GitOps-style continuous deployment.  

---

## Table of Contents

- [Overview](#overview)  
- [About ArgoCD](#about-argocd)  
- [Repository Structure](#repository-structure)  
- [Configuration](#configuration)  
- [Applying Changes](#applying-changes)  

---

## Overview

This repo manages the deployment of Kubeflow in a GitOps workflow. All manifests, Helm values, and environment-specific configurations are stored in Git. Changes to these files can be automatically synchronized to your cluster using ArgoCD, ensuring a reproducible, auditable, and version-controlled deployment.  

---

## About ArgoCD

[ArgoCD](https://argo-cd.readthedocs.io/) is a **declarative, GitOps continuous delivery tool** for Kubernetes. It continuously monitors your Git repository and ensures that the cluster state matches the manifests in the repository.  

**Key responsibilities in this repo:**  
- Watches this repository for changes.  
- Applies updates to the Kubernetes cluster automatically or on-demand.  
- Ensures that the deployed resources match the desired state defined in Git.  

With ArgoCD, any change you commit to this repo will either automatically or manually be applied to your cluster, making deployments predictable and repeatable.  

---

## Repository Structure

├── kubeflow-app-of-apps.yaml
├── sample-values-0.1.5.yaml – Fallback values files.
├── values-overrides-0.1.5.yaml – Final values files. Update this to change deployment parameters.
├── sync_argocd_apps.sh – Bash script to manually trigger ArgoCD synchronization.
└── README.md

---

## Configuration

The main configuration file for Kubeflow is:
```bash
values-overrides-0.1.5.yaml
```

After updating the values file, you must sync the changes with ArgoCD.

## Applying Changes
### Using ArgoCD UI

1. Open the ArgoCD web UI: https://argo-server.kubeflow.uds.ura.go.ug.

2. Click Sync to apply the latest changes from Git.

### Using the Sync Script

A helper script is provided to synchronize all ArgoCD applications defined in this repo:

```bash
bash ./sync_argocd_apps.sh
```