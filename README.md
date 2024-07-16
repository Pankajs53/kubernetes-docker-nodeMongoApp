# Simple Node-Mongo Application

This repository demonstrates how to set up a simple Node.js and MongoDB application using Docker and Kubernetes. The main aim is to showcase the integration of Docker and Kubernetes for container orchestration and deployment.

## Table of Contents

- [Introduction](#introduction)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
  - [Clone the Repository](#clone-the-repository)
  - [Using Pre-Uploaded Docker Image](#using-pre-uploaded-docker-image)
  - [Build and Push Your Own Image](#build-and-push-your-own-image)
  - [Checking Output](#checking-output)
  - [Accessing Kubernetes Dashboard](#accessing-kubernetes-dashboard)
- [Configuration Files](#configuration-files)
- [Contributing](#contributing)
- [License](#license)

## Introduction

This project sets up a basic Node.js application with MongoDB as the database. It includes Docker configurations and Kubernetes manifests to demonstrate containerization and orchestration using these technologies.

## Project Structure

- **Dockerfile**: Defines the Docker image for the Node.js application.
- **host-pv.yml**: Kubernetes Persistent Volume configuration.
- **host-pvc.yml**: Kubernetes Persistent Volume Claim configuration.
- **index.js**: Entry point for the Node.js application.
- **package.json**: Node.js dependencies and scripts.
- **mongo-config.yml**: MongoDB configuration for Kubernetes.
- **mongo-db.yml**: MongoDB deployment and service configuration for Kubernetes.
- **node-app.yml**: Node.js application deployment and service configuration for Kubernetes.

## Prerequisites

- Docker installed on your local machine.
- Kubernetes cluster set up (e.g., Minikube or a cloud provider).

## Getting Started

### Clone the Repository

```bash
git clone https://github.com/Pankajs53/Kubernetes-Docker-NodeApp.git
cd simple-node-mongo-app

### if you wish to use your own image else you can keep the same docker image as it is available on my docker hub

```bash
docker build -t yourusername/node-mongo-app .
docker push yourusername/node-mongo-app

Update the node-app.yml file with your Docker Hub image URL:

```bash
spec:
  containers:
    - name: node-mongo-app
      image: yourusername/node-mongo-app:latest  # Replace with your Docker Hub username and image name
      ports:
        - containerPort: 3000

### Apply the configuration:

```bash
kubectl apply -f mongo-config.yml
kubectl apply -f mongo-db.yml
kubectl apply -f host-pv.yml
kubectl apply -f host-pvc.yml
kubectl apply -f node-app.yml

### Checking Output
** Once deployed, check the Node.js application's service to get the NodePort:

```bash
kubectl get services
minikube service service_name

# Accessing Kubernetes Dashboard
** To view the Kubernetes dashboard, start Minikube's dashboard:

```bash
minikube dashboard



