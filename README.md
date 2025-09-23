# nodejs-demo-app
Sample Node.js app with Docker and CI/CD pipeline
## 🚀 How to Set Up This CI/CD Pipeline

This guide explains how to automate the deployment of a Node.js app using GitHub Actions and Docker.

### 1. Clone or Create Your Node.js App
Ensure your app includes:
- `package.json` with a start script
- `Dockerfile` to containerize the app

### 2. Create a GitHub Repository
Push your project to a new GitHub repo.

### 3. Add a Dockerfile
Place this in your root directory:

```Dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "start"]
EXPOSE 3000


4. Create GitHub Actions Workflow
Inside your repo, create the folder and file:
.github/workflows/main.yml


Paste this workflow:
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


5. Add GitHub Secrets
Go to your repo → Settings → Secrets → Actions:
- DOCKER_USERNAME: your DockerHub username
- DOCKER_PASSWORD: your DockerHub access token

6. Push Code to Trigger CI/CD
Every push to main will:
- Build your Docker image
- Push it to DockerHub automatically

✅ Result
Your app is now containerized and deployed via CI/CD with zero manual steps.







