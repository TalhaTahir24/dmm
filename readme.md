# DMM Kubernetes Infrastructure

This repository contains Kubernetes manifests for deploying and managing core infrastructure components for the DMM project. The setup includes DNS (BIND9), web server (NGINX), and secrets management (Vault), all orchestrated using Kubernetes best practices.

## Repository Structure

```
.
├── bind9/
│   ├── argocd-app.yaml      # ArgoCD application manifest for BIND9
│   ├── configmap.yaml       # BIND9 configuration (ConfigMap)
│   ├── deployment.yaml      # BIND9 Deployment and PVC
│   └── service.yaml         # BIND9 Service
├── nginx/
│   ├── deployment.yaml      # NGINX Deployment
│   ├── ingress.yaml         # NGINX Ingress resource
│   ├── kustomization.yaml   # Kustomize configuration
│   └── service.yaml         # NGINX Service
├── vault/
│   ├── deployment.yaml      # Vault Deployment
│   ├── ingress.yaml         # Vault Ingress resource
│   └── readme.md            # Vault-specific documentation
└── readme.md                # (This file)
```

## Components

### 1. BIND9 (DNS Server)
- **Purpose:** Provides DNS services for the cluster and internal applications.
- **Key Files:**
  - `deployment.yaml`: Deploys BIND9 with persistent storage and config from ConfigMap.
  - `configmap.yaml`: Contains `named.conf` and zone file for `dmm.tt.pk`.
  - `service.yaml`: Exposes BIND9 via Kubernetes Service.
  - `argocd-app.yaml`: For GitOps deployment with ArgoCD.

### 2. NGINX (Web Server)
- **Purpose:** Serves as a web server and ingress point for HTTP traffic.
- **Key Files:**
  - `deployment.yaml`: Deploys NGINX with 3 replicas in the `web` namespace.
  - `service.yaml`: Exposes NGINX via Kubernetes Service.
  - `ingress.yaml`: Configures ingress routing for web traffic.
  - `kustomization.yaml`: For managing resources with Kustomize.

### 3. Vault (Secrets Management)
- **Purpose:** Manages secrets and sensitive data for applications.
- **Key Files:**
  - `deployment.yaml`: Deploys Vault.
  - `ingress.yaml`: Exposes Vault via Ingress.
  - `readme.md`: Vault-specific usage and configuration notes.

## Usage

1. **Clone the repository:**
   ```sh
   git clone https://github.com/TalhaTahir24/dmm.git
   cd dmm
   ```
2. **Apply manifests:**
   Apply the manifests in the desired order, e.g.:
   ```sh
   kubectl apply -f bind9/
   kubectl apply -f nginx/
   kubectl apply -f vault/
   ```
   Adjust namespaces and configurations as needed for your environment.

3. **ArgoCD Integration:**
   Use the `argocd-app.yaml` in the `bind9/` directory for GitOps deployment if using ArgoCD.

## Requirements
- Kubernetes cluster (v1.20+ recommended)
- `kubectl` installed and configured
- (Optional) ArgoCD for GitOps workflows

## Notes
- Update DNS zone files and NGINX ingress rules as per your domain and application requirements.
- Persistent storage is required for BIND9 (see PVC in `bind9/deployment.yaml`).
- Review and secure Vault deployment before using in production.

## License

This repository is maintained by [TalhaTahir24](https://github.com/TalhaTahir24). See individual files for license details if applicable.
Hello
