Nginx Application Deployment Using Kubernetes

1. Project Overview

This project demonstrates deploying an Nginx web application on a local Kubernetes cluster using Minikube.

The application is containerized using Docker and managed by Kubernetes Deployment and Service resources.

The project also demonstrates scaling, self-healing, rolling updates, rollback, and application configuration using ConfigMaps.

2. Project Objectives

- Set up a local Kubernetes cluster using Minikube.
- Deploy Nginx using Kubernetes Deployment.
- Run multiple Nginx Pods.
- Expose the application using Kubernetes NodePort Service.
- Configure a custom HTML webpage using ConfigMap.
- Perform horizontal scaling.
- Test Kubernetes self-healing.
- Perform rolling updates and rollback.
- Troubleshoot Kubernetes application deployment.

3. Technologies Used

Technology| Purpose
Docker| Container runtime
Kubernetes| Container orchestration
Minikube| Local Kubernetes cluster
Nginx| Web server
kubectl| Kubernetes command-line tool
YAML| Kubernetes configuration
HTML| Custom webpage
VS Code| Development environment

4. Architecture

             User Browser
                  |
                  |
           localhost:8080
                  |
                  |
        Kubernetes Port Forward
                  |
                  |
          nginx-service
             (Port 80)
                  |
           Nginx Deployment
                  |
          -----------------
          | |
        Pod 1 Pod 2
          | |
        Nginx Nginx
          | |
          -----------------

       Local Kubernetes Cluster
              Minikube

5. Project Structure

nginx-k8s-lab/
│
├── nginx-deployment.yaml
├── nginx-service.yaml
├── index.html
└── README.md

6. Prerequisites

Install the following tools:

- Docker Desktop
- Minikube
- kubectl
- Visual Studio Code

Verify installations:

docker --version
kubectl version --client
minikube version

7. Start Kubernetes Cluster

Start Docker Desktop.

Execute:

minikube start --driver=docker

Verify cluster:

minikube status
kubectl get nodes

Expected node status:

minikube Ready control-plane

8. Create Custom HTML Webpage

Create an index.html file containing the custom application webpage.

Example:

<!DOCTYPE html>
<html>
<head>
    <title>My Kubernetes Project</title>
</head>
<body>
    <h1>Welcome to My DevOps Project!</h1>
    <h2>Nginx Application Deployed Successfully</h2>
    <p>Running on Kubernetes using Minikube.</p>
    <p>Technology: Docker, Kubernetes and Nginx</p>
</body>
</html>

9. Create ConfigMap

kubectl create configmap nginx-html --from-file=index.html

Verify:

kubectl get configmap

10. Deploy Nginx Application

Apply Deployment configuration:

kubectl apply -f nginx-deployment.yaml

Verify:

kubectl get deployments
kubectl get pods

Expected: Two Nginx Pods running successfully.

11. Expose Application Using Service

Apply Service configuration:

kubectl apply -f nginx-service.yaml

Verify:

kubectl get services

12. Access Application

Execute:

kubectl port-forward service/nginx-service 8080:80

Open browser:

http://localhost:8080

The custom Nginx application should be accessible.

13. Kubernetes Scaling

Scale application from two to four Pods:

kubectl scale deployment nginx-deployment --replicas=4

Verify:

kubectl get pods
kubectl get deployments

Scale down:

kubectl scale deployment nginx-deployment --replicas=2

14. Self-Healing Test

Get Pod names:

kubectl get pods

Delete one Pod:

kubectl delete pod POD_NAME

Watch replacement:

kubectl get pods -w

Kubernetes automatically creates a replacement Pod to maintain the desired replica count.

15. Rolling Update

Update Nginx image:

kubectl set image deployment/nginx-deployment nginx=nginx:1.27-alpine

Check rollout:

kubectl rollout status deployment/nginx-deployment

Verify image:

kubectl get deployment nginx-deployment -o jsonpath="{.spec.template.spec.containers[0].image}"

16. Rollback

Undo the previous deployment update:

kubectl rollout undo deployment/nginx-deployment

Verify:

kubectl rollout status deployment/nginx-deployment
kubectl rollout history deployment/nginx-deployment

17. Troubleshooting Commands

Command| Purpose
kubectl get pods| Check Pod status
kubectl describe pod POD_NAME| Inspect Pod events
kubectl logs POD_NAME| View application logs
kubectl get deployments| Check deployments
kubectl get services| Check Services
kubectl get endpoints nginx-service| Check Service endpoints
kubectl get events| Check cluster events
kubectl get nodes| Check node health

Common errors:

- ImagePullBackOff: Container image download failure.
- CrashLoopBackOff: Container repeatedly crashes.
- Pending: Pod cannot be scheduled.
- Connection refused: Application or network endpoint is not accepting connections.

18. Cleanup

Delete Kubernetes resources:

kubectl delete -f nginx-service.yaml
kubectl delete -f nginx-deployment.yaml
kubectl delete configmap nginx-html

Stop Minikube:

minikube stop

Delete cluster when no longer required:

minikube delete

19. Learning Outcomes

Through this project, I practised:

- Kubernetes cluster management.
- Deployment and Pod management.
- Service networking.
- ConfigMap integration.
- Application scaling.
- Self-healing.
- Rolling updates.
- Rollback and troubleshooting.

20. Project Information

Project: Nginx Application Deployment Using Kubernetes

Environment: Local Minikube Cluster

Cloud Cost: No AWS resources used.

Status: Practical lab and learning project.

---

This project was created as part of my hands-on AWS DevOps and Kubernetes learning journey.
