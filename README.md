This project uses a self-hosted GitHub Actions runner installed on the same
machine where Minikube is running.

When code is pushed to the main branch:
- Docker image is built and pushed automatically
- Kubernetes manifests are applied automatically to Minikube

Note: The runner machine must be online for deployments to work.


Project Overview:

- This project demonstrates an end-to-end CI/CD pipeline to deploy a containerized
Hello World application to Kubernetes using Terraform, Docker, and GitHub Actions.

Terraform - What we Used it for:

- This project uses Terraform with kubernetes provider to demonstrate Infrastructure as Code Concepts.

what Terraform Does in this Project:

- Uses the existig Kubernetes cluster (minikube)
- Connects to cluster using ~/.kube/config
- Validates Kubernetes access through Terraform.
- Demonstrate how Terraform can manage kubernetes resources


Local vs Cloud Explanation:

- For this take-home assignment, the Kubernetes cluster is provisioned locally using
Minikube to avoid cloud cost. The same manifests and pipeline can be reused
without changes for EKS/GKE/AKS.


CI (Continuous Integration):

- Build Docker image

- Push image to Docker Hub

CD (Continuous Deployment):

- Deploy the Docker image to a local Kubernetes cluster (Minikube)

- The entire pipeline is executed using a GitHub self-hosted runner running on the local machine.


Architecture:

Developer Laptop
│
├── GitHub Repository
│ └── GitHub Actions Workflow
│
├── Self-Hosted GitHub Runner (Ubuntu)
│ ├── Docker
│ ├── kubectl
│ └── Minikube (Kubernetes Cluster)
│
└── Docker Hub (Image Registry)


Tech Stack:

	Component 			Tool

	CI/CD				GitHub Actions
	Runner				Self-hosted Github Runner
	Containraization		Docker
	Orchestration			Kubernetes(Minikube)
	Registry			DockerHub
	OS 				Ubuntu

Project Structure:

k8automtion/
│
├── app/
│   ├── index.html
│   └── Dockerfile
│
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
│
├── terraform/
│   ├── main.tf
│   └── variables.tf
│
├── .github/
│   └── workflows/
│       └── ci-cd.yaml
│
└── README.md

Prerequisites:

- Ubuntu 
- Docker Installed
- Minikube Installed
- Kubectl Installed
- Github account 
- Doker Hub Account

Local Environment Setup:

- Start minikube 
	minikube start 
	kubectl get nodes - To verify 
- Setup Github Self-Hosted Runner	
	Go to GitHub Repo - Settings - Actios - Runner
	Add Self Hosted Runner (Linux)
	Follow Github instructions to download and configure runner
- DockerHub Secrete (GitHub)
	To Add following secretes in github repository:
	DOCKER_USERNAME
	DOCKER_PASSWORD

Deployment Flow:

- Developer pushes code to main branch

- GitHub Actions triggers pipeline

- Self-hosted runner executes job

- Docker image is built & pushed

- Kubernetes manifests are applied to Minikube

- Application is deployed successfully


Accessing the Application:

- Check Services - kubectl get svc
- Access via Minikube - minikube service hello-service  [our service name is hello-service]
	or
- Minikube IP - http://192.168.49.2:30007  [minikube-Ip:Node-port]

Why Self-Hosted Runner?

- GitHub-hosted runners cannot access local Minikube clusters

- Self-hosted runner provides:

- Local Kubernetes access

- Full control over infrastructure

- Zero cloud dependency


Status:

- CI Implemented - CD Implemented - Local kubernetes Deployment - Production-Style DevOps Workflow 


