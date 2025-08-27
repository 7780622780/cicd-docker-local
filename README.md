📌 CI/CD Pipeline with GitHub Actions & Docker

📖 Introduction

This project demonstrates a complete CI/CD pipeline using GitHub Actions, Docker, and Docker Hub.
The pipeline automatically builds, tests, and deploys a containerized application on a local VM using Docker Compose.

🎯 Objectives

Automate the build and test process with GitHub Actions

Build and push Docker images to Docker Hub

Deploy the application on a self-hosted runner / local VM

Ensure end-to-end automation from code commit → deployment

🛠️ Tools & Technologies Used

GitHub Actions – CI/CD workflow automation

Docker – Containerization

Docker Hub – Image registry

Docker Compose – Multi-container orchestration

Node.js – Sample application runtime

Self-hosted Runner (Windows/VM) – For local deployment

⚙️ Project Workflow

Run Tests

On every push/PR, GitHub Actions installs dependencies and runs unit tests.

Build & Push Docker Image

On push to main, Docker images are built and tagged with both latest and commit SHA.

Images are pushed to Docker Hub.

Deploy on Local VM

Self-hosted runner pulls the latest Docker image.

docker-compose up -d runs the containerized app.

Health check verifies the app is running.

📂 Repository Structure
.
├── .github/
│   └── workflows/
│       └── ci.yml          # GitHub Actions workflow
|
├── Dockerfile              # Docker image build instructions
├── docker-compose.yml      # Deployment config
├── package.json            # Node.js project config
├── README.md               # Project documentation

🚀 How to Run Locally

Clone the repo:

git clone https://github.com/7780622780/cicd-docker-local

cd cicd-docker-local


Build the Docker image:

docker build -t vignesh1003/cicd-docker-local .


Start with Docker Compose:

docker compose up -d


Verify the app:

curl http://localhost:3000/health

🔗 Docker Hub Repository

Docker Hub – cicd-docker-local

📸 Screenshots (to include)

✅ GitHub Actions successful workflow

✅ Docker Hub image pushed

✅ Running containers (docker ps)

✅ Application running in browser (http://localhost:3000/health)

✅ Grafana home page

📝 Conclusion

This project successfully implements a CI/CD pipeline with GitHub Actions and Docker.
It ensures:

Automated testing, building, and pushing of Docker images

Continuous deployment on a self-hosted runner/local VM

Reliable delivery of containerized applications
