# Python Web Application Deployment with Docker Kubernetes and Jenkins
Python Web Application Deployment – Pro App

This project demonstrates how to build and deploy a Python Flask web application using a complete CI/CD pipeline.
It covers source control integration, automated builds, containerization, image publishing, and deployment to Kubernetes.

The goal of this project is to practice and demonstrate real-world DevOps concepts by building an automated, containerized, and orchestrated deployment pipeline.

# Purpose

To design and implement a fully automated CI/CD pipeline that:

Builds Docker images automatically

Pushes images to DockerHub

Deploys applications to Kubernetes using rolling updates

Ensures fast, repeatable, and reliable deployments


# Tools & Technologies

Language: Python (Flask)

CI/CD: Jenkins

Containerization: Docker

Container Registry: DockerHub

Orchestration: Kubernetes (Minikube)

Version Control: Git & GitHub

Deployment Strategy: Rolling Update

# Pipeline Flow

Developer → GitHub → Jenkins
Jenkins → Docker Build → DockerHub
DockerHub → Kubernetes Deployment → Service (NodePort)
