# Ddoksik Deploy

This repository contains the Kubernetes deployment configurations for the Ddoksik platform. It is structured to manage the deployment of multiple services (UI, Diet, and User) using Kubernetes manifests. The repository utilizes **Kustomize** to manage Kubernetes resources and allows for flexible, reusable configurations across different environments.

## Table of Contents

- [Overview](#overview)
- [Technologies Used](#technologies-used)
- [Directory Structure](#directory-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Service Details](#service-details)
  - [UI Service](#ui-service)
  - [Diet Service](#diet-service)
  - [User Service](#user-service)
- [Ingress Configuration](#ingress-configuration)
- [Kustomize](#kustomize)
- [Contributing](#contributing)
- [License](#license)

## Overview

The Ddoksik platform consists of multiple services, each handling a different part of the application. This repository includes:

- **UI Service**: Frontend interface for the platform.
- **Diet Service**: Backend service managing diet-related logic.
- **User Service**: Backend service handling user information and profiles.

This repository provides Kubernetes deployment, service, and ingress configurations for these services.

## Technologies Used

- **Kubernetes**: An open-source system for automating the deployment, scaling, and management of containerized applications.
- **Kustomize**: A tool to customize Kubernetes resource files.
- **Ingress**: A Kubernetes resource that manages external access to services within a cluster.

## Directory Structure

```bash
ddoksik-deploy/
├── UI/
│   ├── deployment.yaml          # Deployment configuration for the UI service
│   └── service.yaml             # Service configuration for the UI service
│
├── diet/
│   ├── deployment.yaml          # Deployment configuration for the Diet service
│   └── service.yaml             # Service configuration for the Diet service
│
├── user/
│   ├── deployment.yaml          # Deployment configuration for the User service
│   └── service.yaml             # Service configuration for the User service
│
├── ingress/
│   └── ingress.yaml             # Ingress configuration for routing external traffic
│
├── kustomization.yaml            # Kustomize configuration file
├── .gitignore                    # Git ignore file
└── README.md                     # Project documentation
```
Files Breakdown:
deployment.yaml: Defines the Kubernetes deployment for each service (UI, Diet, User).
service.yaml: Exposes each service internally or externally via Kubernetes service.
ingress.yaml: Defines the ingress rules for routing external traffic to the correct service.
kustomization.yaml: The Kustomize configuration that manages overlays and resource customization.
## Installation
Prerequisites
To deploy these configurations, you need:

Kubernetes cluster (local or cloud-based).
kubectl: Kubernetes command-line tool for interacting with the cluster.
Kustomize: Integrated with kubectl, used for customizing Kubernetes resources.
Clone the Repository
Clone this repository to your local machine:

```bash
git clone https://github.com/seungjun-Lee0/ddoksik-deploy.git
cd ddoksik-deploy
```
Kubernetes Setup
Before deploying, ensure your Kubernetes cluster is up and running. Verify it by using the following command:

```bash
kubectl cluster-info
```
Applying the Configurations
Use the kubectl command to apply the Kustomize configurations to your cluster:

```bash
kubectl apply -k .
```
This command will deploy the UI, Diet, and User services, create the corresponding Kubernetes services, and apply the ingress rules for external access.

## Usage
Once the services are deployed, you can access them via the ingress rules defined in the ingress.yaml file. Ensure that you have a functional Ingress Controller (e.g., NGINX Ingress) running in your Kubernetes cluster to route external traffic to the services.

## Service Details
### UI Service
Path: UI/
Files:
deployment.yaml: Defines the deployment for the frontend UI.
service.yaml: Exposes the UI via a Kubernetes service.
### Diet Service
Path: diet/
Files:
deployment.yaml: Defines the deployment for the diet-related backend service.
service.yaml: Exposes the diet service via a Kubernetes service.
### User Service
Path: user/
Files:
deployment.yaml: Defines the deployment for the user-related backend service.
service.yaml: Exposes the user service via a Kubernetes service.
## Ingress Configuration
The ingress.yaml file in the ingress/ directory contains the configuration for routing external traffic to the services. The configuration defines paths for each service, allowing them to be accessed via a single domain or IP with different paths for each service.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ddoksik-ingress
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /ui
        pathType: Prefix
        backend:
          service:
            name: ui-service
            port:
              number: 80
      - path: /diet
        pathType: Prefix
        backend:
          service:
            name: diet-service
            port:
              number: 80
      - path: /user
        pathType: Prefix
        backend:
          service:
            name: user-service
            port:
              number: 80
```
Make sure to update host: example.com to your domain or IP address. This setup will route traffic as follows:

http://example.com/ui → UI Service
http://example.com/diet → Diet Service
http://example.com/user → User Service
## Kustomize
This repository uses Kustomize to manage and apply Kubernetes resource configurations. The kustomization.yaml file defines how the deployment, service, and ingress configurations are combined and applied to the cluster.

To apply the Kustomize configurations:

```bash
kubectl apply -k .
```
To preview the combined resources before applying:

```bash
kubectl kustomize .
```
## Contributing
We welcome contributions to improve the Ddoksik deployment configurations. To contribute:

Fork the repository.
Create a new feature branch (git checkout -b feature-branch).
Commit your changes (git commit -m 'Add new feature').
Push your branch (git push origin feature-branch).
Open a pull request.
Please ensure your code adheres to the project's coding standards.

## License
This project is licensed under the MIT License. See the LICENSE file for more details.
