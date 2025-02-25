# 🚀 FastAPI Dockerized Application with GitHub Actions

## 📑 **Table of Contents**
- [Project Overview](#project-overview)
- [Local Setup and Running](#local-setup-and-running)
- [Building and Running Docker Image](#building-and-running-docker-image)
- [GitHub Actions Workflow Explained](#github-actions-workflow-explained)
- [Docker Token & GitHub Secrets Setup](#docker-token--github-secrets-setup)

---

## 🌟 **Project Overview**
This project demonstrates **Continuous Delivery (CD)** using GitHub Actions for a **Dockerized FastAPI** application. The pipeline:
1. **Builds** the FastAPI Docker image.
2. **Authenticates** with Docker Hub using a **Personal Access Token (DOCKERTOKEN)**.
3. **Pushes** the image to Docker Hub **automatically** upon every `push` to the GitHub repository.

---

## 💻 **Local Setup and Running**
### 🔧 **Prerequisites:**
- Python 3.8+
- pip
- Docker

### ⚡ **Steps to Run Locally:**
```bash
# 1️⃣ Clone the repository
git clone <YOUR_GITHUB_REPO_URL>
cd FastAPi-main/fastapi

# 2️⃣ Install dependencies
pip install -r requirements.txt

# 3️⃣ Run the FastAPI server
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```
Visit: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs) for interactive Swagger UI.

---

## 🐳 **Building and Running Docker Image**
### ⚙️ **Docker Commands:**
```bash
# 1️⃣ Build Docker image
docker build -t <your-dockerhub-username>/fastapi-app:latest .

# 2️⃣ Run the Docker container
docker run -d -p 8000:8000 <your-dockerhub-username>/fastapi-app:latest
```
Your app will now be accessible at [http://localhost:8000](http://localhost:8000).

---

## 🔄 **GitHub Actions Workflow Explained**
Located at: `.github/workflows/docker-image.yml`

### 📝 **Key Steps in Workflow:**
- **Trigger:** On every `push` event.
- **Docker Hub Authentication:**
  ```bash
  echo ${{ secrets.DOCKERTOKEN }} | docker login -u "<your-dockerhub-username>" --password-stdin
  ```
- **Docker Build & Push:**
  ```bash
  docker build -t <your-dockerhub-username>/fastapi-app:latest .
  docker push <your-dockerhub-username>/fastapi-app:latest
  ```

---

## 🔐 **Docker Token & GitHub Secrets Setup**
### 🔑 **Generate Docker Token:**
1. Go to [Docker Hub](https://hub.docker.com/).
2. **Sign in** → **Account Settings** → **Security** → **New Access Token**.
3. **Generate** and copy the token.

### 🔒 **Add GitHub Secret:**
1. Go to your GitHub repository.
2. **Settings** → **Secrets and variables** → **Actions** → **New repository secret**.
3. Add `DOCKERTOKEN` as the **Name** and paste the token in the **Value** field.

---


## 🎯 **Conclusion**
This project showcases **automated Docker image creation and deployment** via **GitHub Actions**, ensuring a smooth **Continuous Delivery** pipeline for FastAPI applications. 🚀✨

