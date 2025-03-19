# 🌦️ WeatherApp - Kubernetes Deployment

## 🔥 Overview
WeatherApp is a cloud-native application deployed on a **Kubernetes KIND (Kubernetes in Docker) cluster**. It consists of multiple microservices, including:
- 🖥️ **Frontend UI (`weatherapp-ui`)** - The user interface for interacting with the app.
- ☁️ **Weather Service (`weatherapp-weather`)** - Fetches weather data from an external API.
- 🔐 **Authentication Service (`weatherapp-auth`)** - Manages user authentication.
- 🗄️ **MySQL Database (`mysql`)** - Stores user authentication data.

## 🏗️ Architecture
The application is deployed using Kubernetes with the following components:
- 📦 **Deployments** for frontend, weather service, and authentication service.
- 🏗️ **StatefulSet** for MySQL to ensure persistent data storage.
- 🌐 **Services** to expose application components.
- 🚪 **Ingress Controller (Nginx)** to manage external access.
- 💾 **Persistent Volumes & StorageClass** to handle database persistence.

The application follows this architecture:
```
+--------------------+      +--------------------+
|  Weather App UI   | <--> |   Auth Service    |
+--------------------+      +--------------------+
           |                          |
           v                          v
+--------------------+      +--------------------+
|  Weather Service  |      |  MySQL Database   |
+--------------------+      +--------------------+
```

## 📋 Prerequisites
Before deploying WeatherApp, ensure you have the following installed:
- 🐳 [Docker](https://www.docker.com/)
- ☸️ [Kubernetes KIND](https://kind.sigs.k8s.io/) or [Minikube](https://minikube.sigs.k8s.io/docs/)
- 🔧 [Kubectl](https://kubernetes.io/docs/tasks/tools/)

## 🔎 Notes
- While this guide focuses on deploying using a **KIND cluster**, you can also use **Minikube** or any other Kubernetes cluster.
- The container images used in this project are built for **ARM architecture**, making them suitable for platforms like Raspberry Pi or Apple Silicon Macs.
- **Secrets and TLS certificates are not included in the repository.** You need to create your own Kubernetes Secrets and provide the required certificates for secure communication.

## 🛠️ Setup KIND Cluster
To create a KIND cluster for this project, run:
```sh
kind create cluster --name weatherapp
```

## 🚀 Deploying WeatherApp
### 1️⃣ Clone the repository
```sh
git clone https://github.com/YOUR_GITHUB_USERNAME/weatherapp.git
cd weatherapp
```

### 2️⃣ Apply Kubernetes manifests
```sh
kubectl apply -f storageclass.yaml
kubectl apply -f statefulset.yaml
kubectl apply -f headless-service.yaml
kubectl apply -f init-job.yaml
kubectl apply -f deployment.yaml
kubectl apply -f deployment\ 2.yaml
kubectl apply -f deployment\ 3.yaml
kubectl apply -f service.yaml
kubectl apply -f service\ 2.yaml
kubectl apply -f service\ 3.yaml
kubectl apply -f ingress.yaml
```

### 3️⃣ Verify Deployment
```sh
kubectl get pods
kubectl get services
kubectl get ingress
```

### 4️⃣ Access the Application
Once deployed, access the application at:
```sh
http://weatherapp.local
```
Ensure that your `/etc/hosts` file has an entry for `weatherapp.local` pointing to your cluster IP.

## ⚙️ Managing the Deployment
### 📈 Scaling Up Services
To scale a deployment (e.g., frontend UI) to 3 replicas:
```sh
kubectl scale deployment weatherapp-ui --replicas=3
```

### 📜 Viewing Logs
To check logs for any service:
```sh
kubectl logs -l app.kubernetes.io/name=weatherapp-ui
```

### 🗑️ Deleting the Deployment
To remove all resources:
```sh
kubectl delete -f .
kind delete cluster --name weatherapp
```
