# K8s WordPress SQL

This repository contains Kubernetes configurations for deploying a WordPress application with a MySQL database. It provides the necessary YAML files for creating and managing the Kubernetes resources required to run WordPress.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation Guide](#installation-guide)
- [Usage](#usage)
- [Configuration](#configuration)
- [License](#license)

## Prerequisites

Before you begin, ensure you have the following installed:

### 1. Install `kubectl`

`kubectl` is the Kubernetes command-line tool.

For most systems, you can follow the official guide:

```bash
# For macOS using Homebrew
brew install kubectl

# For Ubuntu
sudo snap install kubectl --classic

# For Windows using Chocolatey
choco install kubernetes-cli
```

### 2. Install minikube

minikube is a tool that makes it easy to run Kubernetes locally.

For installation, follow these steps:

```bash
# For macOS using Homebrew
brew install minikube

# For Ubuntu
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# For Windows using Chocolatey
choco install minikube
```

### 3. Start Minikube

After installing, start your Minikube cluster:

```bash
minikube start
```

### 4. Install Helm

Helm is a package manager for Kubernetes.

For installation, follow these steps:

```bash
# For macOS using Homebrew
brew install helm

# For Ubuntu
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash

# For Windows using Chocolatey
choco install kubernetes-helm
```

### 5. Install the NGINX Ingress Controller

The NGINX Ingress Controller is essential for managing external access to your services.

Install it using kubectl:

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
```

Verify that the Ingress Controller is running:

```bash
kubectl get pods -n ingress-nginx
```

## Installation Guide

1. **Clone the Repository**

   Open your terminal and clone this repository:

   ```bash
   git clone https://github.com/AdamLevs/K8s-wordpress-sql.git
   cd K8s-wordpress-sql
   ```

2. **Deploy MySQL**

   Create the MySQL Persistent Volume, Persistent Volume Claim, Deployment, and Service:

   ```bash
   kubectl apply -f mysql-pv.yaml
   kubectl apply -f mysql-pvc.yaml
   kubectl apply -f mysql-deployment.yaml
   kubectl apply -f mysql-service.yaml
   ```

3. **Deploy WordPress**

   Create the WordPress Deployment and Service, along with the Ingress:

   ```bash
   kubectl apply -f wordpress-deployment.yaml
   kubectl apply -f wordpress-service.yaml
   kubectl apply -f wordpress-ingress.yaml
   ```

4. **Check the Status of Your Deployments**

   You can check if all the pods are running using:

   ```bash
   kubectl get pods
   ```

   Ensure all pods show a status of Running.

5. **Access WordPress**

   If you're using a cloud provider with a load balancer, you can get the external IP of your Ingress controller:

   ```bash
   kubectl get svc -n ingress-nginx
   ```

   If using minikube, use:

   ```bash
   minikube service wordpress --url
   ```

   Open your web browser and navigate to the IP or hostname specified in your Ingress (e.g., http://wordpress.adamlevs.com).

## Usage

### Setup WordPress

Once the WordPress site is accessible, you will see the WordPress installation page. Follow the instructions to set up your WordPress site. Use the following database credentials:

- Database Name: `wordpress`
- Username: `root`
- Password: `password`
- Database Host: `mysql:3306`

### Manage Your Application

You can manage your WordPress application through the Kubernetes dashboard or via the command line using `kubectl`.

## Configuration

- **MySQL Configuration**: Modify `mysql-deployment.yaml` to change MySQL configurations such as the root password.
- **WordPress Configuration**: Modify `wordpress-deployment.yaml` for additional environment variables related to WordPress.
- **Ingress Configuration**: Modify `wordpress-ingress.yaml` to adjust hostnames or paths.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
