## DevSecOps Automation – End-to-End Solution

This repository is the **umbrella project** for my fully automated, scalable **DevSecOps-GitOps- automation**, designed to demonstrate modern CI/CD, GitOps, Infrastructure as Code (IaC), and integrated security practices.  

The solution leverages **Terraform, Jenkins, Kubernetes (EKS), ArgoCD, Helm, and observability stacks** — all organized into modular repositories for reusability and easy maintenance.  

---

### Repository Structure

This umbrella repo contains submodules pointing to individual projects:

```text
devsecops-automation/
│── devops-tools-setup/         # Jenkins, SonarQube, Dependency-Track, Nexus provisioning
│── java-app-ci/                 # Java application + Jenkins CI pipeline
│── jenkins-shared-library/      # Reusable Jenkins pipeline library
│── eks-setup/                   # AWS EKS cluster provisioning with Terraform
│── java-app-cd/                 # GitOps CD with ArgoCD + Helm + Monitoring
```
---

