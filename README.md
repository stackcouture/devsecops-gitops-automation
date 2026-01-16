## DevSecOps Automation – End-to-End Solution

A production-style DevSecOps + GitOps automation framework that integrates infrastructure provisioning, CI/CD pipelines, security automation, and observability into a modular, reusable setup.  

This project was built end-to-end to replicate enterprise-grade cloud-native delivery on AWS with Terraform, Jenkins, Kubernetes (EKS), ArgoCD, Helm, and monitoring stacks.  

---


## Features  

### Infrastructure as Code  
- **Terraform** for AWS provisioning  
- AWS **EKS**, VPC networking, IAM roles  

### Automated DevOps Tooling  
- **Jenkins** (CI/CD)  
- **SonarQube** (Code Quality & SAST)  
- **Nexus Repository** (Artifact Management)  
- **Dependency-Track** (SCA – Software Composition Analysis)  

### CI/CD Pipelines  
- Jenkins Pipelines with **Shared Library**  
- Java **Spring Boot** application builds & Dockerization  
- Automated scans: **Trivy**, **Snyk**  
- **SBOM** generation + **CoSign** signing  
- Secure credentials via **AWS Secrets Manager**  

### GitOps Continuous Delivery  
- **ArgoCD + Helm** for GitOps CD  
- Multi-environment deployments (**dev/stage/prod**)  
- **ArgoCD ApplicationSets** for scaling environments  

### Observability & Security  
- **Prometheus + Grafana** for monitoring & alerting  
- Dashboards for app & cluster health  
- AI-powered **vulnerability & security reports**  

### DevSecOps Focus  
- **SAST**: SonarQube  
- **SCA**: Dependency-Track, Snyk  
- **Container Security**: Trivy, CoSign  
- **Artifact Security**: Nexus policies + SBOM validation  

---

### Repository Structure

This umbrella repo contains submodules pointing to individual projects:

```text
devsecops-gitops-automation/
│── devops-tools-setup/         # Jenkins, SonarQube, Dependency-Track, Nexus provisioning
│── java-app-ci/                 # Java application + Jenkins CI pipeline
│── jenkins-shared-library/      # Reusable Jenkins pipeline library
│── eks-setup/                   # AWS EKS cluster provisioning with Terraform
│── java-app-cd/                 # GitOps CD with ArgoCD + Helm + Monitoring
```
---

## 🔐 Why DevSecOps?

Traditional CI pipelines focus on delivery speed but often ignore software supply-chain risk, artifact integrity, and deployment trust.

This pipeline overcomes traditional CI limitations by embedding **automated, policy-driven security controls across the entire delivery lifecycle**, from code commit to GitOps-based deployment.

---

### 1️⃣ Security Shifted Left
- Filesystem and dependency scans before image creation  
- Static analysis and quality gates enforced during CI  
- Vulnerabilities detected early, not after release  

---

### 2️⃣ Software Supply-Chain Visibility
- SBOM generation and publication to Dependency-Track  
- Full dependency traceability across application versions  
- Faster response to newly disclosed vulnerabilities  

---

### 3️⃣ Artifact Immutability & Integrity
- Commit-based Docker image tagging  
- Digest-based deployments  
- Guarantees that what is deployed is exactly what was tested  

---

### 4️⃣ Artifact Authenticity
- Container images signed using Cosign  
- Foundation for signature verification before deployment  
- Prevents unauthorized or tampered images from running  

---

### 5️⃣ Multi-Layer Container Security
- Pre-push image scanning (local)  
- Post-push registry scanning (Amazon ECR)  
- Ensures both build-time and registry-level security  

---

### 6️⃣ GitOps-Driven Delivery
- CI produces immutable artifacts  
- CD updates Git as the single source of truth  
- ArgoCD reconciles desired state automatically  

---

### 7️⃣ Controlled Releases
- Manual approval gate before GitOps updates  
- Clear separation of CI and CD responsibilities  
- Safer releases for high-risk changes  

---

> **Note:** This repository represents a *reference DevSecOps implementation*. 

---
### Contributing

Contributions are welcome! Please fork this repo and open a PR.

Areas to contribute:
- Adding more security scanners (e.g., Checkov, tfsec, kube-bench)
- Extending monitoring dashboards
- Optimizing pipelines and GitOps automation

---

### License

This project is licensed under the MIT License – feel free to use and adapt for your organization.

---

### Acknowledgments

Inspired by modern DevSecOps practices from CNCF projects

Thanks to the open-source community for Terraform, Jenkins, ArgoCD, Helm, Prometheus, and Grafana

---
