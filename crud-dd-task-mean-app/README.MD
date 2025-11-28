MEAN Stack CI/CD Deployment – CRUD Application (Docker, Docker Compose, Jenkins)
Project Overview :

This project involves building and deploying a full-stack MEAN (MongoDB, Express, Angular, Node.js) CRUD application.
The application is containerized using Docker & Docker Compose, and completely automated using a CI/CD pipeline in Jenkins, deployed on an AWS EC2 Ubuntu VM.

GitHub Repository Setup:
Created a public GitHub repository.
Cloned the repository locally and added all project files.
Pushed the complete project structure to GitHub

AWS VM Setup:
Launched an Ubuntu 24.04 EC2 instance.
Prepared VPC, subnet, and security group.
Generated a key pair and used the public IP + private key to connect using MobaXterm.
Updated the system packages
sudo apt update && sudo apt upgrade -y

Required Tools Installation:
Installed all mandatory DevOps tools:
Docker
Docker Compose
Nginx
Jenkins

GitProject Code Setup on VM:
Pulled the GitHub repository inside the VM using:
git clone <https://github.com/gowdas1997/crud-dd-task-mean-app.git>

Dockerization:
Backend & Frontend
Created Dockerfiles for both backend and frontend.
Ensured:
Backend exposes port 9090
Frontend (Angular build) served using Nginx inside container
MongoDB
Used official MongoDB Docker image in Docker Compose.

Docker Compose Configuration:
Created a docker-compose.yml with services:
mongodb (official image)
backend
frontend
Linked containers using service names.
Fixed db.config.js to use: mongodb://mongodb:27017/mean-db

Jenkins Setup:
Installed Jenkins and accessed it via browser.
Installed required plugins:
Docker
Docker Pipeline
SSH Agent
Added credentials in Manage Jenkins → Credentials:
Docker Hub username/password
EC2 VM SSH private key

CI/CD Pipeline Creation:
Created a Jenkins Pipeline job with the following stages:
Stage 1 – Checkout Code
Pull latest code from GitHub.
Stage 2 – Build Images
Build backend & frontend Docker images.
Stage 3 – Push to Docker Hub
Push latest images to Docker Hub.
Stage 4 – Deploy on VM
SSH into VM → pull updated images → recreate containers.

Nginx Reverse Proxy Setup:
Configured /etc/nginx/sites-available/default:
/ → Forward to frontend container (8088)
/api → Forward to backend container (9090)
Restarted Nginx: sudo systemctl restart nginx

Final Deployment:
Opened browser: http://<PUBLIC_IP>
Confirmed backend + frontend + database working together.
Successfully added and displayed tutorials from the UI.


