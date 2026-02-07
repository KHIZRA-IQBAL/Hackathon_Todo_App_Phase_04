# Todo App - Phase 4: Kubernetes Deployment

AI-powered conversational todo management application deployed on Kubernetes.

## 🚀 Project Overview

A full-stack todo application with AI chatbot interface built using OpenAI Agents SDK and ChatKit, featuring natural language task management through conversational AI.

## 🛠️ Technology Stack

- **Frontend**: Next.js 14 with OpenAI ChatKit UI
- **Backend**: FastAPI with OpenAI Agents SDK & MCP Server
- **Database**: Neon PostgreSQL (Serverless)
- **Containerization**: Docker & Docker Compose
- **Orchestration**: Kubernetes (Minikube)
- **AI Integration**: OpenAI GPT-4 with MCP Tools

## 📋 Prerequisites

- Docker Desktop (latest version)
- Minikube v1.38+
- kubectl v1.35+
- Node.js 18+
- Python 3.13+

## 📁 Project Structure
```
hackathon-todo-phase4-khizra/
├── frontend/                    # Next.js application
│   ├── src/                    # Source code
│   ├── app/                    # Next.js app router
│   ├── Dockerfile              # Frontend container
│   ├── .dockerignore
│   └── package.json
├── backend/                     # FastAPI application
│   ├── api/                    # API routes
│   ├── models/                 # Database models
│   ├── ai_agent/               # OpenAI agent integration
│   ├── mcp_server/             # MCP server for tools
│   ├── Dockerfile              # Backend container
│   ├── .dockerignore
│   └── requirements.txt
├── k8s/                        # Kubernetes manifests
│   ├── namespace.yaml          # Todo-app namespace
│   ├── secrets.yaml            # Encrypted secrets
│   ├── backend-deployment.yaml # Backend pods
│   ├── backend-service.yaml    # Backend service
│   ├── frontend-deployment.yaml# Frontend pods
│   └── frontend-service.yaml   # Frontend NodePort service
├── docker-compose.yml          # Local development
├── .env.example                # Environment template
└── README.md                   # This file
```

## 🐳 Docker Setup

### Frontend Dockerfile
- Base: `node:18-alpine`
- Installs dependencies with `npm ci`
- Runs in development mode for faster iteration
- Exposes port 3000

### Backend Dockerfile
- Base: `python:3.13-slim`
- Installs FastAPI, Uvicorn, SQLModel, and dependencies
- Copies AI agent and MCP server modules
- Exposes port 8000

### Docker Compose
Orchestrates both services with:
- Network isolation via `todo-network`
- Environment variable injection
- Automatic restart policies

## ☸️ Kubernetes Deployment

### Prerequisites
```bash
# Start Minikube
minikube start

# Verify cluster
kubectl cluster-info
minikube status
```

### Deployment Steps
```bash
# 1. Create namespace
kubectl apply -f k8s/namespace.yaml

# 2. Create secrets (with your actual base64-encoded values)
kubectl apply -f k8s/secrets.yaml

# 3. Deploy backend
kubectl apply -f k8s/backend-deployment.yaml
kubectl apply -f k8s/backend-service.yaml

# 4. Deploy frontend
kubectl apply -f k8s/frontend-deployment.yaml
kubectl apply -f k8s/frontend-service.yaml

# 5. Verify deployments
kubectl get all -n todo-app

# 6. Access the application
minikube service frontend-service -n todo-app --url
```

### Accessing the Application
```bash
# Get frontend URL
minikube service frontend-service -n todo-app

# Or port forward
kubectl port-forward -n todo-app svc/frontend-service 3000:3000
```

Then open `http://localhost:3000` in your browser.

## 🔍 Verification Commands
```bash
# Check pod status
kubectl get pods -n todo-app

# Check services
kubectl get svc -n todo-app

# View logs
kubectl logs -n todo-app deployment/backend-deployment
kubectl logs -n todo-app deployment/frontend-deployment

# Describe resources
kubectl describe deployment backend-deployment -n todo-app
```

## ⚠️ Known Issues

## ⚠️ Known Issues

### ✅ RESOLVED - Docker Build Success
Initial challenges with WSL2/network connectivity were resolved through:
- Fresh Docker Desktop installation with WSL2 integration
- Complete cleanup of previous Docker instances
- Proper .dockerignore files to optimize build performance

**Current Status:** 
- ✅ Both services build successfully
- ✅ Containers run without errors
- ✅ Network connectivity stable
- ✅ Images: Frontend (1.12GB), Backend (763MB)

## 📦 Submission Contents
This Phase 4 submission includes:
- ✅ Complete Dockerfiles (frontend & backend)
- ✅ docker-compose.yml for local testing
- ✅ Kubernetes YAML manifests (6 files)
- ✅ Working K8s deployment architecture
- ✅ Comprehensive documentation

## 🚧 Future Improvements

- [ ] Helm Charts for simplified deployment
- [ ] Horizontal Pod Autoscaling (HPA)
- [ ] Persistent Volume Claims for data
- [ ] Ingress controller for load balancing
- [ ] CI/CD pipeline with GitHub Actions
- [ ] Production-grade image builds

## 👤 Author

**Khizra**  
Hackathon Phase 4 - Kubernetes Deployment

---

**Note**: This project demonstrates containerization and Kubernetes orchestration skills. The application architecture is designed for scalability and cloud-native deployment principles. 
