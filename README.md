# Project Overview
This project delivers a comprehensive framework for automating Continuous Integration and Continuous Deployment (CI/CD) pipelines using Jenkins seamlessly integrated with Amazon Elastic Kubernetes Service (EKS). It aims to simplify application deployment, foster team collaboration, and boost overall productivity.

# 1. Terraform: Infrastructure as Code (IaC)
.Provision an EKS Cluster with two nodes, an Auto Scaling Group, and an Elastic Load Balancer (ELB).

.Deploy an EC2 instance for hosting Jenkins.

.Automate daily snapshots of the Jenkins instance using AWS Backup Service for disaster recovery.

.Save ELB Access Logs to an AWS S3 Bucket for auditing and analysis.
# 2. Ansible: Configuration Management
.Install Jenkins, configure it, and automate plugin installations to ensure a ready-to-use CI/CD server.

.Deploy CloudWatch Agent on all EC2 instances in the project for enhanced monitoring and logging.
# 3. Docker: Containerization
.Build Docker images for the application code to ensure a consistent runtime environment.

.Develop a Docker Compose file to enable the entire application stack to run locally for development and testing.
# 4. Kubernetes: Orchestration and Security
.Write Kubernetes manifests for deploying the application on the AWS EKS Cluster.

.Implement Network Policies to enforce security best practices by controlling communication between pods.
# 5. Jenkins: CI/CD Automation
.Create a pipeline that triggers a build for every push to any branch in the GitHub repository.

Pipeline Stages:
Build the Docker image from the repository's Dockerfile.

Push the Docker image to Dockerhub

Deploy the updated image to the EKS cluster
