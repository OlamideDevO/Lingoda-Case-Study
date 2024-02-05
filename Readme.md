# Symfony Demo App Deployment in Kubernetes

This guide provides step-by-step instructions for deploying the Symfony Demo application in a Kubernetes environment. The instructions cover containerizing the application using Docker, writing Kubernetes manifest files, and ensuring the application is accessible and functional.

## Prerequisites

- Basic understanding of Symfony, Docker, and Kubernetes.
- Access to a Kubernetes cluster.

## Step 1: Obtain Symfony Demo Application

```bash
git clone https://github.com/symfony/demo.git
cd demo




Build and push Docker images for PHP-FPM and Nginx to your container registry. Replace `your-registry` with your actual container registry:

```bash
# Build and push PHP-FPM image
docker build -t your-registry/symfony-app-php-fpm -f Dockerfile.php-fpm .
docker push your-registry/symfony-app-php-fpm

# Build and push Nginx image
docker build -t your-registry/symfony-app-nginx -f Dockerfile.nginx .
docker push your-registry/symfony-app-nginx


Apply Kubernetes manifest files to deploy the Symfony application:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
# If using Ingress
kubectl apply -f ingress.yaml


# Symfony Demo App Deployment in Kubernetes

## Task 2: Implement Database Migrations

### Objective
Add the capability to run database migrations within the Kubernetes deployment from Task 1.

### Instructions

1. **Outline a Process or Create a Script:**

    - Create a new Kubernetes Job YAML file, e.g., `migration-job.yaml`.
    - Use a container image with the Symfony CLI installed (based on PHP image).
    - Mount the application code to the container.
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

    
    
