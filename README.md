# nodejs-demo-app
Sample Node.js app with Docker and CI/CD pipeline
" " 
## 🚀 How I Set Up CI/CD Pipeline with GitHub Actions and Docker

This project demonstrates how I automated the deployment of a Node.js application using GitHub Actions and Docker. Every time I push code to the `main` branch, GitHub automatically builds a Docker image and pushes it to DockerHub — no manual steps required.

### 🧱 Step-by-Step Setup

#### 1. Node.js App Setup
I created a simple Node.js app with a `package.json` and a `Dockerfile`. The `Dockerfile` looks like this:

```Dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "start"]
EXPOSE 3000

2. GitHub Repository
I pushed my project to a GitHub repository and created a workflow file at:
.github/workflows/main.yml


3. GitHub Actions Workflow
This YAML file defines the CI/CD pipeline:
name: CI/CD Pipeline

on:
  push:
    branches: [ "main" ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Log in to DockerHub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build and Push Docker image
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: yourdockerhubusername/your-app-name:latest


4. GitHub Secrets
I added two secrets to my GitHub repository:
- DOCKER_USERNAME: My DockerHub username
- DOCKER_PASSWORD: My DockerHub access token

5. Triggering the Pipeline
Every time I push code to the `main
