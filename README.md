
# GENSaVR Deployment Repository

This repository contains all the deployment manifests created during the integration of GENSaVR into the SPIRIT EU project. GENSaVR is a scalable, interactive training platform designed to simulate real-world laboratory environments. This deployment guide outlines the required services and steps for setting up GENSaVR's infrastructure, ensuring a seamless, collaborative, and data-driven training experience.

## Table of Contents
1. [Requirements](#requirements)
2. [Services Deployment](#services-deployment)
   - [Nakama](#1-nakama)
   - [Mage AI](#2-mage-ai)
   - [AirSignal](#3-airsignal)
   - [Mail Service](#4-mail-service)
3. [Importing MageAI Pipelines](#importing-mage-ai-pipelines)
4. [Enabling an API Trigger for Each Pipeline](#enabling-an-api-trigger-for-each-pipeline)
5. [Overview of Pipelines](#overview-of-pipelines)
6. [Final Words](#final-words)

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

## Importing MageAI Pipelines

Follow these steps to import a pipeline into the Pipelines Dashboard:

1. **Access the Pipelines Dashboard:**  
   Navigate to the Pipelines Dashboard by visiting `/pipelines`.

2. **Create a New Pipeline:**  
   Click the **+ New** button.

3. **Select Import Option:**  
   From the dropdown menu, choose **Import pipeline zip**.

4. **Configure Overwrite Setting (Optional):**  
   - Toggle the **Overwrite pipeline files** option **ON** if you want to replace any existing pipelines or overwrite conflicting block files.
   - If this setting is left **OFF**, new pipelines and block files will be created if they already exist in the project.

5. **Upload the Pipeline File:**  
   - Click the file drop area to **select a file** from your system, or  
   - **Drag and drop** the pipeline zip file into the file drop area.

6. **Start the Import Process:**  
   The pipeline import should begin automatically after uploading the file.

By following these steps, your pipeline will be successfully imported and ready for use.
For more information, visit the official [MageAI Documentation](https://docs.mage.ai/introduction/overview).

## Enabling an API Trigger for Each Pipeline

An **API-type trigger** instructs the pipeline to run when a specific API call is made.

### Steps to Enable an API Trigger:

1. **Create or Edit a Trigger:**
   - Navigate to the trigger section of each pipeline in the UI.
   - Create a new trigger or edit an existing one.

2. **Select API Trigger Type:**
   - Choose **API Trigger** as the trigger type.

3. **Obtain the Endpoint:**
   - After configuring the trigger, the system will provide a **POST endpoint URL**.

4. **Make the API Call:**
   - Send a **POST request** to the provided endpoint when you want to trigger the pipeline.
   - Optionally, include **runtime variables** in your request payload for more customized execution.
  
## Overview of Pipelines

Pipelines in GENSAVR power core features such as object transformations and real-time simulation adjustments. Two primary pipelines have been developed for integration into the system:

1. **Model Transformation Pipeline:**  
   This pipeline performs a **gearwheel cutting operation**, splitting the gearwheel object into two halves. The process automates object manipulation, enabling dynamic adjustments based on simulation needs.

2. **Rotation Application Pipeline:**  
   This pipeline applies a **rotation transformation** to a square object. It adjusts the object's quaternion values to simulate real-time movement, demonstrating object control and physics interactions.

These pipelines enhance the training environment by ensuring responsive, data-driven changes based on user actions and simulation requirements.

## Final Words
By following the steps outlined above, you can deploy GENSaVR's services seamlessly within a Kubernetes cluster. Each service enhances the platform's functionality, ensuring a dynamic, interactive, and scalable training environment for trainees. Additionally, **MageAI** plays a crucial role by enabling real-time data-driven insights and automating object transformations within the training simulations. This integration ensures adaptive learning scenarios, making the training experience more immersive and personalized.

---
