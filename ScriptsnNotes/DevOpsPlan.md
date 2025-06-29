# 🛠️ DevOps Lab Setup Plan (Tim's Home Lab)

---

## ✅ Phase 1: Set Up the DevBox

> Your personal workstation (EC2 instance) for managing infra, Kubernetes, and GitOps workflows.

### Tools to Install:
- Git + GitHub SSH access
- Ansible
- Terraform
- AWS CLI
- `kubectl`
- Helm
- ArgoCD CLI
- Docker (optional)

### Suggested Folder Structure (Git-tracked)

~/git/Home/
├── ansible/
├── terraform/
├── helm/
├── argo/
├── cluster-setup/

Use `.gitkeep` files to track empty folders, and push this structure to your GitHub repo (`tdub777`).

---

## ✅ Phase 2: Provision & Bootstrap Kubernetes Cluster

> Create and configure EC2 instances for your Kubernetes cluster.

### Step 1: Provision EC2 Instances
- 1x DevBox (already done)
- 1x Master node
- 2–3x Worker nodes
- Tags: `role=master`, `role=worker`

🧰 Recommended: Use **Terraform** to create these EC2s

---

### Step 2: Bootstrap Nodes with Ansible
- Install Docker/container runtime
- Set hostnames, disable swap, set sysctl config
- Install **k3s** (or RKE2)
- Join workers to master node
- Install `kubectl` config on DevBox

---

## ✅ Phase 3: Install Rancher (on k3s)

> Use Rancher to visually manage your cluster and workloads.

### Steps:
- Add Helm repo: `rancher-latest`
- Install `cert-manager`
- Deploy Rancher in `cattle-system` namespace
- (Optional) Use Let's Encrypt for real domain + TLS
- Access Rancher via browser

---

## ✅ Phase 4: Install ArgoCD (GitOps)

> Enable continuous delivery to your cluster using Git.

### Steps:
- Deploy ArgoCD via Helm or Kustomize
- Expose via Ingress or port-forward
- Login and configure connection to your GitHub repo (`tdub777`)
- Create `Application.yaml` definitions to sync Helm charts (e.g., Sock Shop)

---

## ✅ Phase 5: Deploy Microservices Demo App

> Use an existing open-source microservice (like Sock Shop) to demonstrate full-stack DevOps workflows.

### Tools & Features:
- Helm charts to deploy services
- ArgoCD to sync Git → cluster
- Logs into **ELK Stack**
- Metrics into **Grafana/Prometheus**
- Optional: Policies via OPA/Gatekeeper

---

## ✅ Phase 6: Add Observability & Security Layers

> Make your platform production-ready (in a lab environment).

### Tools:
- **ELK Stack** for logs (Fluent Bit → Elasticsearch → Kibana)
- **Grafana + Prometheus** for metrics and dashboards
- **Trivy** to scan container images
- **OPA/Gatekeeper** for Kubernetes policies
- **Ingress + TLS** for secure endpoints

---

## ✅ Summary of Major Components

| Category                  | Tools                            |
|---------------------------|----------------------------------|
| Infra Automation          | Terraform, Ansible               |
| Cluster Orchestration     | k3s / RKE2                       |
| Cluster UI / Admin        | Rancher                          |
| GitOps                    | ArgoCD                           |
| Deployment Packaging      | Helm                             |
| App Demo                  | Sock Shop (or other OSS app)     |
| Observability             | ELK Stack, Grafana               |
| Security                  | Trivy, OPA, Gatekeeper           |

---

### 📝 Notes:
- GitHub repo: `https://github.com/tdub777`
- DevBox is your central ops control hub
- Track all automation/scripts/config in Git
- Document everything you deploy for future reuse or interview demonstrations

---
