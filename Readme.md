# Symfony Demo App Deployment in Kubernetes

This guide provides step-by-step instructions for deploying the Symfony Demo application in a Kubernetes environment. The instructions cover containerizing the application using Docker, writing Kubernetes manifest files, scaling, database migration, routing, service discovery and ensuring the application is accessible and functional. 

## Prerequisites

- Basic understanding of Symfony, Docker, and Kubernetes.
- Access to a Kubernetes cluster.

## Step 1: Obtain Symfony Demo Application

```bash
# AWS EC2 instance
# install docker, AWS CLI, Kops cluster and Kubectl

git clone https://github.com/symfony/demo.git
cd demo

Create Dockerfiles to containerize the application

Build and push Docker images for PHP-FPM and Nginx to your container registry. Replace `your-registry` with your actual container registry:

```bash
# Build and push PHP-FPM image
docker build -t symfony-app-php-fpm:latest -f Dockerfile.php-fpm .
docker push your-registry/symfony-app-php-fpm:latest

# Build and push Nginx image
docker build -t symfony-app-nginx:latest -f Dockerfile.nginx .
docker push your-registry/symfony-app-nginx:latest


Apply Kubernetes manifest files to deploy the Symfony application:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
# Using Ingress (routes HTTP traffic based on the requested host)
kubectl apply -f ingress.yaml


# Symfony Demo App Deployment in Kubernetes

## Task 2: Implement Database Migrations

### Objective
Add the capability to run database migrations within the Kubernetes deployment from Task 1.

### Instructions

1. **Outline a Process or Create a Script:**

    - Create a new Kubernetes Job YAML file, e.g., `migration-job.yaml`.
    - Use a container image with the Symfony CLI installed (based on PHP image).
    - The initContainers ensures migrations are executed before the application starts serving traffic, reducing the risk of downtime or data inconsistency.
    - Mount the application code to the container.
    - Mounts volume for application code, required for running migration jobs.
    - Restart policy set to "Never" to ensure the job runs to completion and then terminates.
    - Run Symfony console command for migrations in the Job.

2. **Integrate with Deployment Process:**

    - Modify the deployment YAML (`deployment.yaml`) to include the database migration Job as part of the deployment process.


# Task 3: Scaling Concerns and Implementations

## Objective

Address scaling concerns for the Symfony Demo App in a Kubernetes environment and implement scaling solutions.

## Instructions

### 1. Vertical Scaling

#### a. Adjust Resource Limits

Ensure resource limits are set appropriately for each container in the deployment YAML (`deployment.yaml`). Monitor application performance and adjust resource limits as needed.

Example modification to `deployment.yaml`:

```yaml
resources:
  requests:
    memory: "64Mi"
    cpu: "250m"
  limits:
    memory: "128Mi"
    cpu: "500m"

    
    
