# DevOps Training - Day 6
==========================

## Overview

This session focused on Kubernetes deployment and service configuration using YAML files, followed by hands-on experience with Kubernetes concepts and practical exposure through **Killercoda Labs** and setting up an **EC2 instance**. Additionally, **Jenkins** was introduced as a CI/CD tool to automate Kubernetes deployments.

### Key Learning Highlights:

- **Kubernetes Deployment and Service Configuration**:
  - Deployment YAML file used to define a pod with 5 replicas running the **ipl app** using the Docker image `daviddocker526/ipl-srh:latest` on port 80.
  - Service YAML configured as a **LoadBalancer** (note: LoadBalancer is not supported in Killercoda's free version).
  - Difference between **ClusterIP**, **NodePort**, **LoadBalancer**, and **ExternalName** services in Kubernetes.

- **Jenkins CI/CD Integration**:
  - Jenkins was installed on an **Ubuntu EC2 instance**.
  - Java was installed to support Jenkins.
  - Jenkins was unlocked via the web interface, and necessary plugins were installed.
  - **AWS and Kubernetes** integration through plugins and credentials was set up.
  - A **Jenkins Pipeline** was created to automate deployment scripts to Kubernetes (EKS).

---

## Kubernetes YAML Snippets

### Deployment YAML:
apiVersion: apps/v1

kind: Deployment

metadata:

name: blue-deploy

namespace: blue-ns

spec:

replicas: 5


selector:
matchLabels:

app: ipl

template:

metadata:

labels:

app: ipl

spec:
containers:

- name: c-1
- image: daviddocker526/ipl-srh:latest

ports:
- containerPort: 80

  
### Service YAML:
apiVersion: v1

kind: Service

metadata:

name: blue-service

namespace: blue-ns

spec:

selector:

app: ipl

ports:
- protocol: TCP
  
port: 80


targetPort: 80

type: LoadBalance


---

## Key Kubernetes Commands Practiced

- **Create a namespace**:
kubectl create ns blue-ns

- **Apply Deployment YAML**:
kubectl apply -f blue-deployment.yaml

- **Get all resources in the namespace**:
kubectl get all -n blue-ns

- **Delete Deployment**:

kubectl delete deployment blue-deploy -n blue-ns

- **Delete Service**:
kubectl delete svc blue-service -n blue-ns

---

## Jenkins Installation on Ubuntu EC2 Instance

### Steps:

1. **Update system and install dependencies**:
sudo su

apt update -y

sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update

sudo apt-get install jenkins

sudo apt install default-jdk -y

3. **Install AWS CLI and kubectl on Jenkins server**:
sudo apt install unzip -y

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

unzip awscliv2.zip

sudo ./aws/install

aws configure

---

## Jenkins and Kubernetes Integration

### Steps:

1. **AWS CLI and kubectl Configuration**:
- Installed awscli and kubectl on the Jenkins server.
- Configured AWS credentials via `aws configure`.

2. **Setup EKS Access**:
- Copied the kubeconfig file from the EKS cluster to the Jenkins user.
- Added the kubeconfig as a global Jenkins credential.

3. **Jenkins Pipeline Setup**:
- Created a Jenkins Pipeline job.
- Added scripts to automate the deployment process to EKS.

---


