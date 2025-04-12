# DevOps Training - Day 5
==========================

## Overview

Day 5 of the DevOps training focused on **Kubernetes (K8s)**, a powerful container orchestration and management tool that addresses the limitations of Docker. We covered the drawbacks of Docker, explored Kubernetes features, architecture, and set up a Kubernetes cluster on AWS using **eksctl**. The hands-on experience enabled us to work with **Pods**, **ReplicaSets**, and **Namespaces**, learning how to manage containerized applications in a scalable, resilient way.

---

## Drawbacks of Docker

While Docker provides great benefits for containerization, it does have some limitations:

- **No self-maintenance of containers**.
- **Cannot handle load balancing**.
- **No support for auto-scaling**.

These challenges led to the introduction of **Kubernetes**, a solution for managing and orchestrating containers at scale.

---

## Kubernetes (K8s)

### **What is Kubernetes?**

Kubernetes (often abbreviated as K8s) is an open-source container orchestration platform for automating the deployment, scaling, and management of containerized applications. It was introduced by **Google** and donated to the **Cloud Native Computing Foundation (CNCF)** in 2014.

### **Key Features of Kubernetes**

1. **Auto-scaling**: Automatically scales up/down based on traffic.
2. **Auto-healing**: Automatically restores deleted resources.
3. **Load balancing**: Distributes traffic evenly across containers.
4. **Platform independent**: Runs on any OS.
5. **Rollback**: Reverts to previous versions if needed.
6. **Health monitoring**: Continuously checks the health of containers.
7. **Fault tolerance**: Alerts when nodes fail.
8. **Orchestration**: Manages and coordinates containerized applications.

---

##  Kubernetes Architecture

### **Cluster**

A Kubernetes cluster is a combination of nodes, which are of two types:

1. **Master Node**: 
   - **API Server**: Entry point for all Kubernetes API requests.
   - **etcd**: Key-value store for configuration data.
   - **Controller Manager**: Ensures the cluster's desired state is maintained.
   - **Scheduler**: Assigns workloads (pods) to worker nodes.

2. **Worker Node**:
   - **Kubelet**: Ensures containers are running in a Pod.
   - **Pod**: The smallest deployable unit in Kubernetes, containing one or more containers.
   - **Container Engine**: Runs the containers.
   - **Kube-proxy**: Manages network configuration and traffic routing.

---

## Cluster Setup

### Steps to Set Up Kubernetes Cluster

1. **Launch EC2 Instance**
   - Choose **Ubuntu**, **t2.medium**, 25GB storage, with SSH and HTTP enabled.

2. **Connect and Update**
   -sudo su
   -apt update -y

3. **Install kubectl (Kubernetes CLI)**
  - curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
  -sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
  -chmod +x kubectl
  -mkdir -p ~/.local/bin
  -mv ./kubectl ~/.local/bin/kubectl
  -kubectl version --client

4. **Install eksctl (For Ubuntu)**
  -ARCH=amd64
  -PLATFORM=$(uname -s)$ARCH
  -curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"
  -tar -xzf eksctl$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz
  -sudo mv /tmp/eksctl /usr/local/bin

5. **Install AWS CLI**
  -apt install unzip -y
] -curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
  -unzip awscliv2.zip
  -sudo ./aws/install
  -aws --version

6. **Configure AWS CLI**
Create an IAM user with AdministratorAccess policy and generate access keys. Then configure AWS CLI:
aws configure


7. **Create Kubernetes Cluster**
Run the following command to create the Kubernetes cluster:

eksctl create cluster --name blue-cluster --region sa-east-1 --zone sa-east-1a,sa-east-1b --nodegroup-name red-node --node-type t2.medium --node 2


---

## Kubernetes Namespace Creation

### Imperative Method
kubectl create namespace white
kubectl get namespace


### Declarative Method (YAML)
Create a YAML file (`blue.yaml`) with the following content:
apiVersion: v1
kind: Namespace
metadata:
name: white-2

Apply the YAML file:

---

##  Create a Pod Using YAML

Create a YAML file (`blue-pod.yaml`) with the following content:
apiVersion: v1
kind: Pod
metadata:
name: blue-pod2
namespace: white-2
spec:
containers:
- name: c-1
image: daviddocker526/ipl
ports:
- containerPort: 80


---

## ReplicaSet

Create a YAML file (`white-replica.yaml`) with the following content:
apiVersion: apps/v1
kind: ReplicaSet
metadata:
name: blue-replica1
namespace: white-2
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
- name: c-2
image: daviddocker526/ipl
ports:
- containerPort: 80



---

## Alternative: Use KillerCoda Playground

For an alternative setup, use Kubernetes 1.32 lab on KillerCoda Playground. Login with Google; each session lasts for one hour.

---


   
