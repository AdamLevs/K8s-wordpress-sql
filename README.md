# WordPress & MySQL on Kubernetes

A Helm chart that deploys WordPress with MySQL database on Kubernetes, providing a scalable and persistent blog platform.

## What's Included
- WordPress deployment with configurable replicas
- MySQL database using StatefulSet with persistent storage
- Secure password management via Kubernetes Secrets
- Services for internal communication
- Optional Ingress for external access

## Usage

### Installation
```bash
# Clone the repository
git clone https://github.com/username/helm-chart_Wordpress+SQL.git
cd helm-chart_Wordpress+SQL.git

# Configure deployment (create values.yaml)
cat > values.yaml << EOF
mysql:
  storage: 10Gi
  rootPassword: change-this-password

wordpress:
  replicaCount: 2
  service:
    type: ClusterIP
  ingress:
    enabled: true
    host: wordpress.example.com
EOF

# Deploy with Helm
helm install my-wordpress .
```

### Accessing WordPress
- If Ingress is enabled: Navigate to the hostname you configured
- Without Ingress: `kubectl port-forward svc/wordpress 8080:80`
- Then visit http://localhost:8080

### Cleanup
```bash
helm uninstall my-wordpress
```
