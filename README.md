

# Real-Time Chat Application

## 📝 Introduction

This project aims to provide a real-time chat experience that's both scalable and secure. With a focus on modern technologies, we're building an application that's easy to use and maintain.

## ✨ Features


* **Real-time Messaging**: Send and receive messages instantly using Socket.io 
* **User Authentication & Authorization**: Securely manage user access with JWT 
* **Scalable & Secure Architecture**: Built to handle large volumes of traffic and data 
* **Modern UI Design**: A user-friendly interface crafted with React and TailwindCSS 
* **Profile Management**: Users can upload and update their profile pictures 
* **Online Status**: View real-time online/offline status of users 


## 🛠️ Tech Stack


* **Backend:** Node.js, Express, MongoDB, Socket.io
* **Frontend:** React, TailwindCSS
* **Containerization:** Docker
* **Orchestration:** Kubernetes (planned)
* **Web Server:** Nginx
* **State Management:** Zustand
* **Authentication:** JWT
* **Styling Components:** DaisyUI


### 🔧 Prerequisites


* **[Node.js](https://nodejs.org/)** (v14 or higher)
* **[Docker](https://www.docker.com/get-started)** (for containerizing the app)
* **[Git](https://git-scm.com/downloads)** (to clone the repository)




🐳 Docker Setup

Build Images
docker build -t <your-dockerhub-username>/chat-backend ./backend

docker build -t <your-dockerhub-username>/chat-frontend ./frontend

Push to Docker Hub
docker push <your-dockerhub-username>/chat-backend

docker push <your-dockerhub-username>/chat-frontend


🔁 CI/CD Pipeline

Code pushed to GitHub triggers Jenkins pipeline

Jenkins builds Docker images

Images are pushed to Docker Hub

Kubernetes deployment is updated automatically


☸️ Kubernetes Deployment

Apply Kubernetes Manifests

kubectl apply -f k8s/

Verify Deployment

kubectl get pods

kubectl get services

🌐 Access Application
kubectl get svc frontend-service

Open the EXTERNAL-IP in your browser.




📈 Future Enhancements

Implement Ingress Controller for domain-based routing

Add Helm charts for better deployment management

Integrate Prometheus & Grafana for monitoring

Enable auto-scaling using HPA

Secure application using Kubernetes Secrets










