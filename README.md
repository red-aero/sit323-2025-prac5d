# SIT323 5.2D: Deploying a Dockerized Microservice to Google Cloud

This README outlines the steps to build, tag, push, and verify your Dockerized Node.js microservice using **Google Cloud Artifact Registry**.

## 📌 Overview

This project involves deploying a Dockerized microservice to a private container registry on Google Cloud. You will:

- Enable and configure Google Artifact Registry.
- Build the Docker image locally.
- Tag and push the image to Artifact Registry.
- Verify and optionally run the image from the registry.

---

## 📁 Project Details

- **Project ID:** `sit323-25t1-harshit-216b697`  
- **Artifact Registry Location:** `us-central1-docker.pkg.dev/sit323-25t1-harshit-216b697/sit323-container-registry`  
- **Image Name:** `sit323-2025-prac5p:latest`

---

## ✅ Prerequisites

- Google Cloud SDK (`gcloud`) installed.
- Docker installed and running.
- A GCP project with billing enabled.
- Artifact Registry API enabled.
- Basic knowledge of Docker and GCP.

---

## 🚀 Deployment Steps

### 1. Enable Artifact Registry API
```bash
gcloud services enable artifactregistry.googleapis.com
```

### 2. Authenticate Docker with Artifact Registry
```bash
gcloud auth configure-docker us-central1-docker.pkg.dev
```

---

### 3. Build the Docker Image
In your project directory (where `Dockerfile` is located):
```bash
docker build -t sit323-2025-prac5p:latest .
```

---

### 4. Tag the Image for Artifact Registry
```bash
docker tag sit323-2025-prac5p:latest us-central1-docker.pkg.dev/sit323-25t1-harshit-216b697/sit323-container-registry/sit323-2025-prac5p:latest
```

---

### 5. Push the Image to Artifact Registry
```bash
docker push us-central1-docker.pkg.dev/sit323-25t1-harshit-216b697/sit323-container-registry/sit323-2025-prac5p:latest
```

---

### 6. Verify Image in Registry
```bash
gcloud artifacts docker images list us-central1-docker.pkg.dev/sit323-25t1-harshit-216b697/sit323-container-registry
```

---

### 7. Pull the Image from the Registry
To test on any machine:
```bash
docker pull us-central1-docker.pkg.dev/sit323-25t1-harshit-216b697/sit323-container-registry/sit323-2025-prac5p:latest
```

---

### 8. Run the Image Locally
```bash
docker run -d -p 3000:3000 us-central1-docker.pkg.dev/sit323-25t1-harshit-216b697/sit323-container-registry/sit323-2025-prac5p:latest
```

Visit: `http://localhost:3000`

---

## 🛠️ Troubleshooting

### Authentication Issues
Ensure you're logged in:
```bash
gcloud auth login
gcloud auth configure-docker us-central1-docker.pkg.dev
```

Manual login (if needed):
```bash
gcloud auth print-access-token | docker login -u oauth2accesstoken --password-stdin https://us-central1-docker.pkg.dev
```

---

### Permission Errors
Ensure your IAM roles include:
- `Artifact Registry Writer`
- `Storage Admin`

Also verify your project:
```bash
gcloud config set project sit323-25t1-harshit-216b697
```

---

### Tag Format
Ensure your image tag format follows:
```
us-central1-docker.pkg.dev/<PROJECT_ID>/<REPO>/<IMAGE_NAME>:<TAG>
```

---
