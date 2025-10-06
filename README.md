# DevOps Assessment - Next.js Containerized Application

A containerized Next.js application deployed to Kubernetes using Docker, GitHub Actions, and Minikube.

## 🚀 Features

- Multi-stage Docker build for optimized image size
- Automated CI/CD pipeline with GitHub Actions
- Kubernetes deployment with health checks
- Production-ready configuration

## 📋 Prerequisites

- Node.js 20+ and npm
- Docker Desktop
- Minikube
- kubectl
- Git

## 🛠️ Local Development

### 1. Clone the Repository

```bash
git clone https://github.com/Jp2op/next.js-devops-assesment.git
cd next.js-devops-assesment
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Run Development Server

```bash
npm run dev
```

Visit `http://localhost:3000` to see your application.

## 🐳 Docker

### Build Docker Image Locally

```bash
docker build -t nextjs-app:local .
```

### Run Docker Container Locally

```bash
docker run -p 3000:3000 nextjs-app:local
```

Visit `http://localhost:3000` to access the containerized application.

## 🔄 GitHub Actions CI/CD

The GitHub Actions workflow automatically:
1. Builds the Docker image on push to `main` branch
2. Pushes the image to GitHub Container Registry (GHCR)
3. Tags images with:
   - `latest` (for main branch)
   - Branch name
   - Git SHA

### Setup GHCR Access

1. The workflow uses `GITHUB_TOKEN` automatically
2. Make sure your repository is public or configure package visibility
3. Image will be available at: `ghcr.io/jp2op/next.js-devops-assesment:latest`

## ☸️ Kubernetes Deployment with Minikube

### 1. Start Minikube

```bash
minikube start --driver=docker
```

### 2. Update Deployment Image

Edit `k8s/deployment.yaml` and replace my username with your GitHub username:

```yaml
image: ghcr.io/jp2op/next.js-devops-assesment:latest
```


### 3. Deploy to Kubernetes

```bash
# Apply deployment
kubectl apply -f k8s/deployment.yml

# Apply service
kubectl apply -f k8s/service.yml
```

### 4. Verify Deployment

```bash
# Check pods
kubectl get pods

# Check deployment
kubectl get deployment nextjs-app

# Check service
kubectl get service nextjs-service
```

### 5. Access the Application

#### Using Minikube Service

```bash
minikube service nextjs-service
```

This will automatically open the application in your browser.


## 📊 Monitoring

### View Logs

```bash
kubectl logs -f deployment/nextjs-app
```

### Check Pod Health

```bash
kubectl describe pod <pod-name>
```

### Scale Deployment

```bash
kubectl scale deployment nextjs-app --replicas=5
```

## 🧹 Cleanup

### Delete Kubernetes Resources

```bash
kubectl delete -f k8s/
```

### Stop Minikube

```bash
minikube stop
minikube delete
```

## 📁 Project Structure

```
.
├── .github/
│   └── workflows/
│       └── docker-build.yml    # CI/CD pipeline
├── k8s/
│   ├── deployment.yaml         # Kubernetes deployment
│   └── service.yaml            # Kubernetes service
├── app/                        # Next.js app directory
├── public/                     # Static assets
├── Dockerfile                  # Multi-stage Docker build
├── .dockerignore              # Docker ignore rules
├── next.config.js             # Next.js configuration
├── package.json               # Node.js dependencies
└── README.md                  # Documentation
```

## 🔧 Configuration Details

### Docker Optimization
- Multi-stage build reduces image size
- Node Alpine base image (~40MB vs ~900MB)
- Standalone output for minimal runtime dependencies
- Non-root user for security
- Layer caching optimization

### Kubernetes Features
- **3 replicas** for high availability
- **Resource limits** to prevent resource exhaustion
- **Liveness probe** to detect and restart unhealthy containers
- **Readiness probe** to manage traffic routing
- **NodePort service** for external access

### Health Checks
- Liveness: Checks every 10s, restarts after 3 failures
- Readiness: Checks every 5s, removes from service after 3 failures

## 🔗 Links

- **Repository**: https://github.com/Jp2op/next.js-devops-assesment.git
- **GHCR Image**: ghcr.io/jp2op/next.js-devops-assesment:latest

## 📝 License

MIT

## 👤 Author

Jp - DevOps Assessment Submission
This project was created as a part of assigment from WEXA AI