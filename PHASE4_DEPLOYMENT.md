# Phase 4: Local Kubernetes Deployment Guide

## 🎯 Overview

This guide covers deploying the Todo AI Chatbot to a local Kubernetes cluster using Minikube, Docker, and Helm.

## ✅ Prerequisites Installed

- ✅ Docker Desktop (v29.1.3)
- ✅ Minikube (v1.37.0)
- ✅ kubectl (v1.34.1)
- ✅ Helm (installing...)
- ✅ WSL 2 (Ubuntu)

## 📁 Project Structure

```
todo-hackathon/
├── api/
│   ├── Dockerfile              # Backend Docker image
│   ├── .dockerignore
│   └── index.py               # FastAPI app with /health endpoint
├── web-app/
│   ├── Dockerfile              # Frontend Docker image
│   ├── .dockerignore
│   └── next.config.js         # Updated for standalone output
├── helm/
│   └── todo-app/
│       ├── Chart.yaml          # Helm chart metadata
│       ├── values.yaml         # Configuration values
│       └── templates/
│           ├── frontend-deployment.yaml
│           ├── frontend-service.yaml
│           ├── backend-deployment.yaml
│           ├── backend-service.yaml
│           ├── secrets.yaml
│           └── ingress.yaml
└── scripts/
    ├── deploy-local.bat       # Windows deployment script
    └── cleanup.bat            # Cleanup script
```

## 🚀 Deployment Steps

### Step 1: Start Minikube

```powershell
# Start Minikube with Docker driver
minikube start --driver=docker

# Verify status
minikube status
```

### Step 2: Configure Docker Environment

```powershell
# Point Docker CLI to Minikube's Docker daemon
minikube docker-env --shell powershell | Invoke-Expression
```

### Step 3: Build Docker Images

```powershell
# Build Frontend
cd web-app
docker build -t todo-frontend:latest .
cd ..

# Build Backend
cd api
docker build -t todo-backend:latest .
cd ..
```

### Step 4: Create Kubernetes Secrets

```powershell
# Create secret from .env file
kubectl create secret generic todo-secrets --from-env-file=api\.env
```

### Step 5: Deploy with Helm

```powershell
# Install/upgrade the application
helm upgrade --install todo-app .\helm\todo-app `
  --set frontend.image.pullPolicy=Never `
  --set backend.image.pullPolicy=Never `
  --wait
```

### Step 6: Access the Application

```powershell
# Get service URLs
minikube service todo-frontend --url
minikube service todo-backend --url

# Or open in browser directly
minikube service todo-frontend
```

## 🤖 Automated Deployment (Recommended)

Use the automated script for one-command deployment:

```powershell
# Run the deployment script
.\scripts\deploy-local.bat
```

This script will:
1. ✅ Check Minikube status (start if needed)
2. ✅ Configure Docker environment
3. ✅ Build both Docker images
4. ✅ Create Kubernetes secrets
5. ✅ Deploy with Helm
6. ✅ Wait for pods to be ready
7. ✅ Display access URLs

## 🔍 Verification Commands

```powershell
# Check pods status
kubectl get pods

# Check services
kubectl get services

# Check deployments
kubectl get deployments

# View frontend logs
kubectl logs -l app=todo-frontend

# View backend logs
kubectl logs -l app=todo-backend

# Describe a pod (for troubleshooting)
kubectl describe pod <pod-name>
```

## 🧹 Cleanup

To remove the deployment:

```powershell
# Using cleanup script
.\scripts\cleanup.bat

# Or manually
helm uninstall todo-app
kubectl delete secret todo-secrets
```

## 🐛 Troubleshooting

### Issue: Pods not starting

```powershell
# Check pod status
kubectl get pods

# View pod logs
kubectl logs <pod-name>

# Describe pod for events
kubectl describe pod <pod-name>
```

### Issue: Image pull errors

Make sure you're using Minikube's Docker daemon:

```powershell
minikube docker-env --shell powershell | Invoke-Expression
docker images  # Should show todo-frontend and todo-backend
```

### Issue: Database connection errors

Check if secrets are created:

```powershell
kubectl get secrets
kubectl describe secret todo-secrets
```

### Issue: Service not accessible

```powershell
# Check service status
kubectl get services

# Use minikube tunnel (if needed)
minikube tunnel
```

## 📊 Architecture

```
┌─────────────────────────────────────────────┐
│           Minikube Cluster                  │
│                                             │
│  ┌──────────────┐      ┌──────────────┐   │
│  │  Frontend    │      │   Backend    │   │
│  │  (Next.js)   │─────▶│  (FastAPI)   │   │
│  │  Port: 3000  │      │  Port: 8000  │   │
│  │  Replicas: 2 │      │  Replicas: 2 │   │
│  └──────────────┘      └──────────────┘   │
│         │                      │           │
│         └──────────┬───────────┘           │
│                    │                       │
│            ┌───────▼────────┐              │
│            │    Secrets     │              │
│            │  (DB, API Keys)│              │
│            └────────────────┘              │
│                                             │
└─────────────────────────────────────────────┘
                    │
                    ▼
            External Access
         (minikube service)
```

## 🎯 Key Features

- **Multi-replica deployment**: 2 replicas each for frontend and backend
- **Health checks**: Liveness and readiness probes configured
- **Resource limits**: CPU and memory limits set
- **Secrets management**: Environment variables stored securely
- **Service discovery**: Internal DNS for service-to-service communication
- **Rolling updates**: Zero-downtime deployments with Helm

## 📝 Configuration

Edit `helm/todo-app/values.yaml` to customize:

- Replica counts
- Resource limits
- Environment variables
- Service types
- Image tags

Example:

```yaml
frontend:
  replicaCount: 3  # Increase replicas
  resources:
    limits:
      memory: "1Gi"  # Increase memory
```

Then redeploy:

```powershell
helm upgrade todo-app .\helm\todo-app
```

## 🔐 Security Notes

1. **Secrets**: Never commit `.env` files to Git
2. **RBAC**: Consider adding Role-Based Access Control for production
3. **Network Policies**: Add network policies to restrict pod communication
4. **Image Scanning**: Scan Docker images for vulnerabilities before deployment

## 📚 Next Steps

- [ ] Add monitoring with Prometheus
- [ ] Set up logging with ELK stack
- [ ] Implement CI/CD pipeline
- [ ] Deploy to cloud (Phase 5)
- [ ] Add horizontal pod autoscaling
- [ ] Implement service mesh (Istio/Linkerd)

## 🆘 Support

If you encounter issues:

1. Check pod logs: `kubectl logs <pod-name>`
2. Describe resources: `kubectl describe <resource-type> <name>`
3. Check Minikube status: `minikube status`
4. Restart Minikube: `minikube delete && minikube start`

---

**Ready to deploy? Run `.\scripts\deploy-local.bat` and you're good to go! 🚀**
