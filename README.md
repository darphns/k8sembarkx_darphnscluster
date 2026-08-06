# Kubernetes Microservices & Deployment Portfolio

This repository contains a collection of Kubernetes deployments and microservice architectures, demonstrating progression from basic container orchestration to complex, multi-tier internal networking.

## Repository Structure

* **`app1_hello/`**: Foundational deployment testing basic Kubernetes Pod creation and container lifecycle management.
* **`demo/`**: A standalone Spring Boot application deployment demonstrating environment configuration and single-service routing.
* **`tax-app2/`**: A decoupled microservice architecture featuring a frontend web application and a backend tax calculation engine. 

## Technical Stack
* **Orchestration:** Kubernetes (K8s)
* **Containerization:** Docker
* **Framework:** Spring Boot (Java)
* **Environment:** WSL2 / Linux

## Key Architecture & Networking Concepts Implemented
* **Internal Pod-to-Pod Communication:** Configured `ClusterIP` services to allow seamless, secure data transfer between the frontend and backend microservices (`tax-app2`).
* **External Traffic Routing:** Implemented `NodePort` services to expose frontend applications to external user traffic.
* **Declarative Infrastructure:** Managed all deployments, services, and environment variables using Kubernetes YAML manifests.
* **Service Discovery & DNS:** Debugged and resolved strict label selector mismatches to ensure K8s Endpoints correctly mapped to active Pods for reliable internal DNS resolution.

## How to Run

Navigate to any specific project directory and apply the configuration files to your cluster:

1. Start your local cluster (e.g., Docker Desktop / Minikube).

	## 🛠️ Essential Command Cheatsheet

Here is the exact sequential workflow used to deploy, debug, and manage these microservices:

**1. Deployment**
* Apply all YAML configurations in the current directory:
  `kubectl apply -f .`
* Check the status of all running resources (Pods, Services, Deployments):
  `kubectl get all`

**2. Networking & Verification**
* List all active Services and their assigned internal/external IPs:
  `kubectl get svc`
* Inspect a specific Service (crucial for verifying if Endpoints are mapping to Pods correctly):
  `kubectl describe svc <service-name>`

**3. Debugging**
* View the logs for a specific running Pod:
  `kubectl logs <pod-name>`
* Filter massive log outputs to instantly find Java stack trace errors:
  `kubectl logs <pod-name> | grep -i "Exception"`

**4. Teardown & Resource Management**
* Gracefully destroy all K8s resources defined in the current directory:
  `kubectl delete -f .`
* Reclaim local storage by purging unused Docker images and dead containers:
  `docker system prune -a --volumes`
