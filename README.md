# DevSecOps + GitOps Automation

A modular, end-to-end DevSecOps + GitOps framework demonstrating secure, traceable, and auditable cloud-native delivery. Built with AWS, Kubernetes, Jenkins, Argo CD, Helm, and Terraform.

This is **hands-on platform engineering**—not demos, not tutorials.

---
## Demo Flow
![Demo GIF](demos/demo-end-to-end.gif)

---

## Features  

### Infrastructure as Code
- AWS provisioning using **Terraform** (EKS, VPC, IAM, networking)  
- Reproducible environments across **dev, stage, and prod**

### CI/CD Pipelines
- Jenkins pipelines with **shared library**  
- Build, test, and package Java Spring Boot apps  
- **Shift-left security**: SAST (SonarQube), SCA (Dependency-Track, Snyk), filesystem scans  
- Docker image creation with **commit-based tagging**  
- Multi-layer container security: pre-push & post-push scanning (Trivy)  
- Image signing with **Cosign** for artifact authenticity  
- Secure credentials via **AWS Secrets Manager**

### GitOps Continuous Delivery
- **Argo CD + Helm** for multi-environment deployment  
- **ApplicationSets** for scalable environment management  
- Promotion workflow via GitHub Actions (dev → stage → prod)  
- Automatic reconciliation ensures environments match Git

### Observability
- **Prometheus + Grafana** dashboards for app and cluster health  
- Centralized security and compliance reports

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

## Design Principles

Our platform engineering approach is guided by the following core principles:

### Shift-Left Security
Detect and address security issues early in the development lifecycle, before artifacts are released.

### Immutable Artifacts
Ensure artifacts are built once and deployed exactly as tested, preventing drift and inconsistencies.

### GitOps First
Adopt declarative deployments to eliminate manual interventions and maintain a single source of truth.

### Supply-Chain Security
Verify trust at both build and deployment time to secure the entire software supply chain.

### Auditability & Transparency
Maintain complete visibility over all changes, builds, and security scans for compliance and traceability.

---

> **Note:** This repository represents a *reference DevSecOps implementation*. 

---
## How It Works

### CI Pipeline
- Builds, tests, runs security scans, generates SBOM, and builds & signs Docker images.

### Artifact Management
- Pushes artifacts to Amazon ECR using immutable digest-based tags.

### Environment Promotion
- CI updates Git values files.
- GitHub Actions manage promotion across environments.

### CD with Argo CD
- ApplicationSets deploy environments automatically.
- Self-healing and drift detection ensure consistency.

### Security & Observability
- Multi-layer security scans.
- Prometheus and Grafana dashboards provide monitoring and insights.

---

## Limitations

- Pipeline execution is slower due to multiple scans; better suited for main/gated branches.  
- Single pipeline combines CI/CD/security; production-grade platforms should split responsibilities.  
- Security thresholds depend on tooling and require continuous tuning.  
- Manual approval gates do not scale; policy-driven automation is recommended.  
- Some values are hardcoded for demo clarity; shared platforms require full parameterization.

---

## How I’d Evolve This at Scale

- **Separate Pipelines:** Split CI, security scans, and CD into independent pipelines for maintainability and parallel execution.  
- **Policy-Driven Approvals:** Replace manual gates with automated security and compliance checks.  
- **Dynamic Environments:** Automate ephemeral environments for feature branches using ApplicationSets.  
- **Centralized Security Dashboard:** Aggregate SAST, SCA, and container scan results into a single observability platform.  
- **Scaling GitOps:** Integrate multiple repositories with mono-/multi-tenant strategies for enterprise workloads.  
- **Enhanced Artifact Registry:** Implement artifact promotion policies and lifecycle management beyond ECR.
---

### Contributing

Contributions are welcome! Please fork this repo and open a PR.

Areas to contribute:
- Adding more security scanners (e.g., Checkov, tfsec, kube-bench)
- Extending monitoring dashboards
- Optimizing pipelines and GitOps automation

---

### License

You are free to use, copy, modify, merge, publish, distribute, sublicense and/or sell copies of the software, subject to the conditions in the license.

This project is provided under a **view-only** license for review and portfolio purposes.  
See the [LICENSE](./LICENSE) file for details.

---

### Acknowledgments

Inspired by modern DevSecOps practices from CNCF projects

Thanks to the open-source community for Terraform, Jenkins, ArgoCD, Helm, Prometheus, and Grafana

---
