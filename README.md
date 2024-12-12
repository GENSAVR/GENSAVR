
# GENSaVR Deployment Repository

This repository contains all the deployment manifests created during the integration of GENSaVR into the SPIRIT EU project. GENSaVR is a scalable, interactive training platform designed to simulate real-world laboratory environments. This deployment guide outlines the required services and steps for setting up GENSaVR's infrastructure, ensuring a seamless, collaborative, and data-driven training experience.

## Table of Contents
1. [Requirements](#requirements)
2. [Services Deployment](#services-deployment)
   - [Nakama](#1-nakama)
   - [Mage AI](#2-mage-ai)
   - [AirSignal](#3-airsignal)
   - [Mail Service](#4-mail-service)
3. [Final Words](#final-words)

---

## Requirements
- **Docker**
- **Kubernetes Cluster**

---

## Services Deployment

### 1. Nakama
Nakama enhances GENSaVR with real-time multiplayer features, enabling scalable and interactive training environments. Trainees can participate in collaborative or competitive lab simulations, with customizable matchmaking and session management that dynamically adjusts based on skill levels and training progress. Nakama is central to the authentication process of GENSaVR, serving as the primary repository for user data while also enabling seamless matchmaking functionality.

#### Deployment Steps
1. Navigate to the `nakama_deployment` folder.
2. Apply each manifest using the following commands in the recommended order:

```bash
kubectl apply -f postgres-pvc.yaml
kubectl apply -f postgres-statefulset.yaml
kubectl apply -f postgres-service.yaml
kubectl apply -f nakama-pvc.yaml
kubectl apply -f nakama-deployment.yaml
kubectl apply -f nakama-service.yaml
```

#### Access Nakama Dashboard
Open the Nakama dashboard by visiting [http://localhost:7351](http://localhost:7351) in your browser.

---

### 2. Mage AI
Mage AI simplifies the creation, deployment, and management of data pipelines for machine learning and analytics. Its API-first approach supports various cloud platforms and data sources, making it ideal for dynamic and personalized training simulations.

#### Benefits of Integration
- **Realistic and Adaptive Simulations:** Accurate object transformations and responsive environments.
- **Dynamic Interactions:** Real-time responses based on trainee actions and progression.
- **Enhanced Learning:** Personalized simulations improve engagement and learning outcomes.

#### Deployment Steps
1. Navigate to the `mage_deployment` folder.
2. Replace the placeholder path `/path/to/mage_project` in the config file with your desired Mage project path.
3. Deploy the application using the following command:

```bash
kubectl create -f mage.yaml
```

#### Check Pod Status
```bash
kubectl get pods -o wide
```

#### Port Forwarding
```bash
kubectl port-forward mage-server 6789:6789
```

#### Access Mage Dashboard
Open the Mage dashboard by visiting [http://localhost:6789](http://localhost:6789) in your browser.

---

### 3. AirSignal
AirSignal facilitates real-time WebRTC-based communication within GENSaVR, enabling live audio features for collaborative training sessions, instructor feedback, and seamless multi-user interactions.

#### Deployment Steps
1. Navigate to the `airsignal_deployment` folder.
2. Apply the manifests using the following commands:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

---

### 4. Mail Service
The MailService is a Python-based microservice designed to handle email-based password resets securely. Users interact with this service indirectly through the GENSaVR client when they click the "Reset Password" button.

#### Deployment Steps
1. Navigate to the `mail_service_deployment` folder.
2. Apply the deployment manifest using the following command:

```bash
kubectl apply -f deployment.yaml
```

---

## Final Words
By following the steps outlined above, you can deploy GENSaVR's services seamlessly within a Kubernetes cluster. Each service enhances the platform's functionality, ensuring a dynamic, interactive, and scalable training environment for trainees.

---
