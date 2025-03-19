# Weather App on Kubernetes ☁️🚀

## Overview
This is a **microservices-based weather application** deployed on **Kubernetes**. It consists of authentication, weather data retrieval, and a web UI, all running inside a scalable and secure Kubernetes environment.

## Features
✅ **Authentication Service** – Handles user login and authentication. 🔐  
✅ **Weather Service** – Fetches real-time weather data from an external API. ☁️  
✅ **User Interface** – A web frontend for users to interact with the app. 🎨  
✅ **MySQL Database** – Stores user authentication details. 🗄️  
✅ **Kubernetes Deployment** – Uses Deployments, StatefulSets, Ingress, and Secrets for a cloud-native setup. ⚙️  
✅ **Ingress with TLS** – Secures external access to the UI. 🔒  

## Architecture
```
+-------------------+     +-------------------+
|  Weather App UI  | <-> |  Auth Service     |
+-------------------+     +-------------------+
       |                        |
       v                        v
+-------------------+     +-------------------+
|  Weather Service |     |  MySQL Database  |
+-------------------+     +-------------------+
```

## Deployment
To deploy this project on Kubernetes, follow these steps:

1️⃣ **Clone the repo**
```bash
git clone https://github.com/yourusername/weatherapp-k8s.git
cd weatherapp-k8s
```

2️⃣ **Apply Kubernetes manifests**
```bash
kubectl apply -f manifests/
```

3️⃣ **Access the application**
- If using **Ingress**, open `https://weatherapp.local`
- If using **NodePort**, get the external IP:
```bash
kubectl get svc weatherapp-ui
```

## Security Considerations
🔴 If deploying in a real environment, **do not store secrets in GitHub**. Use external secrets management like **Kubernetes Secrets** or **HashiCorp Vault**.

