Project Overview
This project demonstrates a comprehensive DevOps pipeline with a focus on automation, containerization, and orchestration using cutting-edge tools and technologies. Below are the key components and their contributions:

1. Terraform: Infrastructure as Code (IaC)
.Provision an EKS Cluster with two nodes, an Auto Scaling Group, and an Elastic Load Balancer (ELB).
.Create an RDS Instance for the database, with credentials stored securely in AWS Secrets Manager.
.Deploy an EC2 instance for hosting Jenkins.
.Automate daily snapshots of the Jenkins instance using AWS Backup Service for disaster recovery.
.Save ELB Access Logs to an AWS S3 Bucket for auditing and analysis.
2. Ansible: Configuration Management
.Install Jenkins, configure it, and automate plugin installations to ensure a ready-to-use CI/CD server.
.Deploy CloudWatch Agent on all EC2 instances in the project for enhanced monitoring and logging.
3. Docker: Containerization
.Build Docker images for the application code to ensure a consistent runtime environment.
.Develop a Docker Compose file to enable the entire application stack to run locally for development and testing.
4. Kubernetes: Orchestration and Security
.Write Kubernetes manifests for deploying the application on the AWS EKS Cluster.
.Implement Network Policies to enforce security best practices by controlling communication between pods.
5. Jenkins: CI/CD Automation
.Create a pipeline that triggers a build for every push to any branch in the GitHub repository.
Pipeline Stages:
Build the Docker image from the repository's Dockerfile.
Push the Docker image to Dockerhub
Deploy the updated image to the EKS cluster
