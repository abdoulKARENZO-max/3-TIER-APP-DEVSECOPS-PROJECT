Hands-on experience with a production-ready 3-tier DevSecOps & GitOps Architecture on AWS EKS.Hands-on experience with a production-ready 3-tier DevSecOps & GitOps Architecture on AWS EKS.
A Fully Automated, Enterprise grade deployment of a Three-Tier application (React Frontend, Node.js Backend, and MongoDB Database) on Amazon Elastic Kubernetes Service (EKS) on a Cloud-native basis. This project is a showcase of modern cloud-based practices that involve shifting security left and applying pull-based continuous delivery (GitOps).
 A short version (less than 300 words):
 Architecture Overview

The infrastructure is deployed using AWS EKS and kubernetes clusters are kept in private subnets. An AWS Application Load Balancer (ALB) is used for all traffic routes that are external to the AWS Cloud. Resources are declared by Terraform in modular configurations, using S3 for remote state locking. PersistentVolumes (PV) are a Kubernetes resource for managing database persistence, supported by AWS Elastic Block Storage (EBS).
 DevSecOps Pipeline
Security is applied on the commit, not on the deployment. Each code push initiates a 4-phase GitHub Actions workflow:
1. SonarCloud – static code analysis against enterprise quality gates.
3. ProCode — static code analysis of signed code to detect unpatched vulnerabilities.4. App Security — automated code scanning for app vulnerabilities.
3. Docker Build — Application built into smallest possible container images
5. Trivy — deep image layer scan, image is tagged and pushed to DockerHub if there is no high/critical vulnerability

 Using ArgoCD for GitOps Delivery.

Manual deployments of the type `kubectl` are completely gone. ArgoCD is deployed within the cluster and periodically checks the Git repository. ArgoCD checks for the drift between the desired and live image, and performs a zero-downtime rolling update without any manual effort.

 Observability
The standard CNCF stack (Prometheus scrapes metrics from the EKS control plane and worker nodes, Grafana visualizes CPU, memory, network and capacity data on custom dashboards) is used for cluster-wide monitoring using Helm.
 Key Outcomes
- No local CI overhead and automated multi-stage CI/CD with managed cloud workers
Lock in, drift-resistent deployments using GitOps state management
Solved various real-world problems like AWS IAM permissions, Route53 DNS propagation, and ALB target-group routing.


