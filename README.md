# CI/CD with GitHub Actions & Docker (No Cloud Needed)

This repo demonstrates a full CI/CD pipeline that builds a Docker image, runs tests, pushes to Docker Hub, and deploys locally using either **Docker Compose** or **Minikube**.

## What you get
- Node.js Express sample app with `/`, `/health`, and `/version`
- Jest tests
- `Dockerfile` and `docker-compose.yml`
- Kubernetes manifests for Minikube (`k8s/app.yaml`)
- Single GitHub Actions workflow that: tests -> builds -> pushes -> deploys (to a **self-hosted** runner on your local VM)

## Prerequisites
- Docker & Docker Compose installed on your **local VM / laptop**
- (Optional) Minikube + kubectl if you prefer K8s
- Docker Hub account + a repo named `cicd-docker-local`
- GitHub repository for this code
- A **self-hosted GitHub Actions runner** installed on your local VM (for the deploy step)

### 1) Fork or push this repo to GitHub
Create a new GitHub repo and push these files.

### 2) Create Docker Hub repo
- Create a public repo named `cicd-docker-local` under your Docker Hub username.

### 3) Add GitHub Secrets
In your GitHub repo → **Settings → Secrets and variables → Actions → New repository secret** add:
- `DOCKERHUB_USERNAME` – your Docker Hub username
- `DOCKERHUB_TOKEN` – a Docker Hub Access Token

### 4) Update deploy target
- In `docker-compose.yml` and `k8s/app.yaml`, replace `DOCKERHUB_USERNAME` with your actual Docker Hub username. The workflow also auto-replaces this during deploy.

### 5) Install a self-hosted runner on your local VM
Follow GitHub docs: Settings → Actions → Runners → New self-hosted runner.
- On your VM run the provided commands from GitHub to download & configure the runner.
- Start the runner: `./run.sh`
- Ensure Docker is available to that runner user.

### 6) Run the pipeline
- Push to `main` branch → tests run → image builds & pushes → local deploy via Compose.
- Verify locally: `curl http://localhost:3000/health` should return `{ "status": "ok" }`.

### 7) Minikube path (optional)
- Start minikube: `minikube start`
- Replace `DOCKERHUB_USERNAME` in `k8s/app.yaml`
- Apply: `kubectl apply -f k8s/app.yaml`
- Access: `minikube service cicd-docker-local --url` or `http://$(minikube ip):30080`

### Screenshots to capture
- GitHub Actions workflow green checks
- Docker Hub repo showing pushed tags (`latest` and commit SHA)
- Running container: `docker ps` and browser `http://localhost:3000/`
- (If K8s) `kubectl get pods,svc` and the app in browser via NodePort

---

**Note**: The workflow uses a self-hosted runner for deploy (so it deploys to your local VM). If you do not want auto-deploy, you can disable the `deploy_compose` job or trigger it manually using `workflow_dispatch`.
