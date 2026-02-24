# MEAN Stack Deployment on AWS using Docker & CI/CD

This repository contains a full-stack CRUD application built with the **MEAN** stack. The project demonstrates containerization, orchestration, and automated deployment (CI/CD) to a cloud environment.

---

## 📋 Project Requirements Fulfilled

* **Containerization**: Separate Dockerfiles for Frontend and Backend.
* **Orchestration**: Docker Compose for multi-container management.
* **Reverse Proxy**: Nginx configuration for unified routing.
* **CI/CD**: GitHub Actions pipeline for automated builds.
* **Cloud Hosting**: Deployed on AWS EC2 instance.

---

## 🏗 System Architecture

The application is orchestrated using four interconnected containers:

| Container | Role | Port (Internal) |
| :--- | :--- | :--- |
| **nginx-proxy** | Entry point & Reverse Proxy | 80 |
| **mean-frontend** | Angular UI (Served via Nginx) | 80 |
| **mean-backend** | Node.js/Express API | 8080 |
| **mongodb** | NoSQL Database | 27017 |



---

## 🚀 Deployment Instructions

### 1. Local Setup
To run the environment locally for development:
```bash
git clone <your-repo-url>
cd <repo-folder>
docker-compose up -d


2. CI/CD Pipeline (GitHub Actions)
The workflow is defined in .github/workflows/main.yml. On every push to the main branch:

The code is linted and tested.

Docker images are built for Frontend and Backend.

Images are pushed to Docker Hub under the namespace sagarpatade1900/.



3. Production Deployment (AWS EC2)
To update the live environment:

SSH into the EC2 instance.

Navigate to the app directory.

Execute the update sequence:

Bash
docker-compose pull
docker-compose up -d --force-recreate


🛠 Technical Challenges & Solutions
Challenge 1: Nginx Default Page Conflict
Issue: The "Welcome to Nginx" default page was showing instead of the Angular app.

Solution: Updated the Docker volume mapping to overwrite /etc/nginx/conf.d/default.conf and ensured the Angular dist path matched the Nginx root directory inside the container.

Challenge 2: API Connection (CORS/Localhost)
Issue: Frontend could not reach the backend because it was pointing to localhost:8080.

Solution: Configured Nginx as a reverse proxy. Changed the Angular baseUrl to a relative path (/api), allowing Nginx to route traffic internally between containers.



🔗 Project Links
Live Demo: http://13.233.45.141

Docker Hub (Frontend): sagarpatade1900/mean-frontend

Docker Hub (Backend): sagarpatade1900/mean-backend
