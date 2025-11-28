## Overview

This project is a MEAN stack application deployed using Docker, Docker Compose, Nginx, and a complete CI/CD pipeline using GitHub Actions with a self-hosted runner on AWS EC2.

It includes:

Angular frontend

Node.js backend

MongoDB database

Nginx reverse proxy

Automated CI/CD pipeline

## Project Structure
DiscoverDollar/
├── docker-compose.yml
├── .github/workflows/deploy.yml
└── crud-dd-task-mean-app/
    ├── backend/
    │   └── Dockerfile
    └── frontend/
        ├── Dockerfile
        └── nginx.conf

## Dockerized Services

# Frontend

Angular app

Built using Node.js builder image

Served using Nginx

# Backend

Node.js (Express API)

Connects to MongoDB

# Database

MongoDB official Docker image

Networking

All services run inside the same Docker network (app-network).

## How to Run Locally

1. Clone Repo
git clone https://github.com/<your-username>/DiscoverDollar.git
cd DiscoverDollar

2. Run with Docker Compose
docker-compose up --build

## Deploying on AWS EC2 With CI/CD 

To deploy this project on AWS using CI/CD, an Ubuntu EC2 instance is created and Docker and Docker Compose are installed on it. A GitHub self-hosted runner is then configured on the EC2 server so GitHub Actions can run the pipeline directly on the machine. In the GitHub repository, two secrets (DOCKER_USERNAME and DOCKER_PASSWORD) are added to allow the pipeline to log in to Docker Hub. Whenever code is pushed to the main branch, GitHub Actions automatically builds the backend and frontend Docker images, pushes them to Docker Hub, and then the EC2 runner uses Docker Compose to pull the latest images and deploy the updated containers. This automates the entire deployment process on AWS.

## CI/CD Pipeline (GitHub Actions)

The workflow (deploy.yml) performs:

Checkout source code

Build backend Docker image

Push backend image to Docker Hub

Build frontend Docker image

Push frontend image

Deploy using Docker Compose on the EC2 runner