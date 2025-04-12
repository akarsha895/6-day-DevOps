# DevOps Training - Day 4

## Overview

Day 4 of the DevOps training focused on the pivotal role of **DevOps engineers** and **testers** in the deployment process. The session provided an in-depth look at **Docker** and its integration into the DevOps pipeline. We explored how multiple developers' code is integrated, containerized using Docker, and deployed to production environments. The hands-on experience enabled us to understand containerization, Docker image building, and deployment on EC2 instances.

---

## Docker Containerization

We began by diving into **Docker**, a powerful containerization tool that simplifies application deployment by packaging the source code, dependencies, and libraries into a single unit — a container. We explored the following Docker components:

1. **Dockerfile**: A text file containing instructions for building Docker images.
2. **Docker Image**: Created from a Dockerfile, containing the app and its dependencies.
3. **Docker Registry**: A repository for storing Docker images, such as **DockerHub**.
4. **Docker Container**: A running instance of a Docker image.

### **Dockerfile Example**

We created a simple **Dockerfile** to install **Apache2** and serve a basic web application. The file includes instructions for installing dependencies, copying the app to the appropriate directory, and exposing port 80.

```dockerfile
FROM ubuntu:latest
WORKDIR /COLOR
RUN apt-get update -y
RUN apt-get install apache2 -y
COPY . /var/www/html
EXPOSE 80
CMD ["apache2ctl", "-D", "FOREGROUND"]
 EC2 Ubuntu Instance Setup
We launched an EC2 Ubuntu instance and installed Docker to containerize the application. We followed these steps:

Launch EC2 Instance: Choose Ubuntu as the operating system.

Install Docker:

We installed Docker using the following commands:

sudo apt-get update -y
sudo apt-get install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker
Build Docker Image: We built the Docker image for the web application:

docker image build -t <name> .
Run Docker Container: We ran the Docker container, exposing port 80:

docker run -d --name <container> -p <host_port>:80 <image>
Managing Docker Containers
We practiced managing Docker containers using various commands:

View Running Containers:

docker ps
View Logs:

docker logs <container>
Pause, Unpause, Stop, Restart, Remove Containers:

Pause:

docker pause <container>
Unpause:

docker unpause <container>
Stop:

docker stop <container>
Restart:

docker restart <container>
Remove:

docker rm <container>
 Accessing Deployed Application
After successfully deploying the container on port 81, we configured the AWS security groups to allow external traffic and accessed the application using the public IP and port.

Security Group Configuration
We ensured that the security group allowed traffic on port 81, enabling access to the web application from external networks.

 DockerHub Integration
We created a DockerHub account and learned how to push and pull Docker images to and from DockerHub:

Tag and Push Docker Image:

docker tag green-v2:latest akarsha895/green-v2:latest
docker push akarsha895/green-v2:latest
Pull Docker Image: We practiced pulling images from DockerHub:

docker pull akarsha895/green-v2:latest
 Deploying Public Docker Images
We explored deploying public Docker images directly from GitHub repositories, such as daviddocker526/ipl:

Accessing Deployed Images: We accessed the deployed application using its public IP:

http://3.39.226.214:86/
Accessing Running Containers: We used the following command to interact with the container’s shell:

docker exec -it <container> bash
This allowed us to navigate the deployed application files.
