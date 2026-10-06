Markdown
# 🚀 Production-Grade Automated CI/CD Pipeline

A fully automated DevOps pipeline designed to continuously integrate, analyze, containerize, and deploy a web application with zero manual intervention. Built using **Jenkins, SonarQube, Docker, and AWS Elastic Container Registry (ECR)**.

---

## 📌 Project Overview

This project demonstrates a real-world continuous deployment flow where every code push to the `main` branch automatically triggers a declarative multi-stage Jenkins pipeline.

The pipeline performs code checkouts, static analysis for quality and security gates, builds container images with unique dynamic tagging, pushes remote artifacts to AWS ECR, and executes an automated container lifecycle deployment on the server.

---

## 🛠️ Tech Stack & Tools Used

- **Source Control:** Git & GitHub
- **CI/CD Automation:** Jenkins (Declarative Pipeline)
- **Code Quality & Security:** SonarQube Scanner
- **Containerization:** Docker Engine
- **Cloud Registry:** AWS ECR (Elastic Container Registry)
- **Infrastructure / Host:** AWS EC2 (Amazon Linux 2023)

---

## 🏗️ Architecture & Pipeline Flow

[ Developer Push ] ──> [ GitHub Repo ]
│
▼
[ Jenkins Pipeline ]
│
┌───────────────────────┼───────────────────────┐
▼                       ▼                       ▼

Source Checkout   2. SonarQube Analysis    3. Docker Image Build
│                                               │
└───────────────────────┬───────────────────────┘
▼
4. AWS ECR Authentication
│
▼
5. Push Image to AWS ECR
│
▼
6. Automated Docker Deploy (-p 8081:80)


---

## ⚙️ Pipeline Stages Breakdown

1. **Source Code Checkout:** Pulls the latest commits from the GitHub repository.
2. **Workspace Inspection:** Verifies working directory, permissions, and required deployment files (`Dockerfile`, `sonar-project.properties`).
3. **Static Code Analysis (SonarQube):** Analyzes code smells, bugs, and security vulnerabilities before proceeding to build.
4. **Build Container Image:** Builds a lightweight Nginx-based Docker image tagged with the dynamic Jenkins `${BUILD_NUMBER}`.
5. **Authenticate AWS ECR:** Retrieves authorization credentials via AWS CLI using securely configured Jenkins credentials (`aws-creds`).
6. **Publish to AWS ECR:** Tags and pushes the verified image to the private AWS ECR repository (`ap-south-1`).
7. **Deploy Application:** Automatically cleans up any previously running application container and spins up the newly built container version on port `8081`.

---

## 📁 Repository Structure

```text
├── Dockerfile                  # Production Nginx image configuration
├── Jenkinsfile                 # Declarative multi-stage pipeline configuration
├── sonar-project.properties    # SonarQube analysis configuration
├── index.html                  # Responsive portfolio web application
└── README.md                   # Project documentation
🚀 How to Run Locally
If you want to test and run the application locally without Jenkins:

Clone the repository:

Bash
git clone [https://github.com/shd-zone/jenkins-portfolio.git](https://github.com/shd-zone/jenkins-portfolio.git)
cd jenkins-portfolio
Build the Docker image:

Bash
docker build -t devops-portfolio:local .
Run the container:

Bash
docker run -d -p 8081:80 --name my-portfolio devops-portfolio:local
Open your browser and navigate to http://localhost:8081.

👤 Author
Shaikh Shahid

GitHub: @shd-zone

Role: DevOps & Cloud Engineering Aspirant