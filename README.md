# 📦 GitHub Actions CI Pipeline for React App

This repository contains a **React application** with a complete **CI pipeline** built using **GitHub Actions** and a **self-hosted runner**.

---

## 🚀 CI Pipeline Stages

### 🔹 Stage 1 – Checkout
- Uses `actions/checkout` to pull source code into the runner.  
- Verifies that the runner is working.  

---

### 🔹 Stage 2 – SonarQube Scan
- Runs **SonarQube analysis** on the codebase.  
- Configured with `sonar-project.properties`.  
- Performs **Quality Gate check** (set as non-blocking).  

---

### 🔹 Stage 3 – React Build (npm)
- Installs dependencies using `npm install`.  
- Builds React app using `npm run build`.  
- Uploads `build/` directory as an artifact.  
- Fixed **OpenSSL issue** with Node.js by adjusting version/flags.  

---

### 🔹 Stage 4 – Trivy File Scan
- Runs **Trivy FS Scan** on project files.  
- Detects vulnerabilities in source code and dependencies.  
- Uploads scan results as an artifact.  

---

### 🔹 Stage 5 – OWASP Dependency Check (Skipped)
- Planned for dependency vulnerability analysis.  
- Currently **skipped** in pipeline.  

---

### 🔹 Stage 6 – Docker Build
- Builds a **Docker image** for the React app.  
- Tagged as `sivahere/git-actions-img:latest`.  

---

### 🔹 Stage 7 – Trivy Image Scan
- Runs **Trivy Image Scan** on the built Docker image.  
- Detects OS package and library vulnerabilities inside the image.  
- Uploads scan report as an artifact.  

---

### 🔹 Stage 8 – Push to DockerHub
- Authenticates to DockerHub using GitHub Secrets.  
- Pushes the Docker image → `sivahere/git-actions-img:latest`.  

---

## ⚙️ Prerequisites

- **Self-hosted GitHub Actions runner** (Ubuntu EC2).  
- **Docker** installed on the runner EC2.  
- **Trivy** installed on the runner EC2.  
- **SonarQube server** running (on a separate EC2 or server).  
- GitHub Secrets configured:  
  - `SONAR_TOKEN`  
  - `SONAR_HOST_URL`  
  - `DOCKERHUB_USERNAME`  
  - `DOCKERHUB_PASSWORD`  

---

## 📊 Pipeline Flow


    A[Stage 1: Checkout] --> B[Stage 2: SonarQube Scan]
    B --> C[Stage 3: React Build]
    C --> D[Stage 4: Trivy File Scan]
    D --> E[Stage 6: Docker Build]
    E --> F[Stage 7: Trivy Image Scan]
    F --> G[Stage 8: Push to DockerHub]

<img width="1474" height="665" alt="image" src="https://github.com/user-attachments/assets/7f8713a2-4e96-4449-9adb-8cb847d9ca48" />
<img width="940" height="767" alt="image" src="https://github.com/user-attachments/assets/37fa6287-753c-4db6-84e7-9da7efb234ff" />




    
