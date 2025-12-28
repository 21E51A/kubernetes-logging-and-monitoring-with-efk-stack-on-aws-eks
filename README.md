# Kubernetes Logging & Monitoring with EFK Stack on AWS EKS

This project demonstrates a **centralized logging and monitoring solution** for Kubernetes workloads using the **EFK stack**:  
- **Elasticsearch** – log storage and indexing  
- **Fluent Bit** – log collection and forwarding  
- **Kibana** – log visualization  

The project is deployed on **AWS EKS** with multiple nodes, persistent storage, and secure networking.

---

## Project Overview

- **Cluster:** AWS EKS, multi-node, public/private subnets  
- **Log Collector:** Fluent Bit deployed as DaemonSet  
- **Log Storage:** Elasticsearch cluster with StatefulSet and Persistent Volumes (EBS)  
- **Visualization:** Kibana dashboards for real-time log monitoring  
- **Networking:** NodePort and LoadBalancer services, security groups configured  

![Kibana Dashboard](screenshots/kibana-dashboard.png)  <!-- Add your screenshot here -->

---

## Features

- Collects logs from all Kubernetes pods  
- Centralized storage in Elasticsearch  
- Real-time visualization and dashboards in Kibana  
- Persistent storage for Elasticsearch using EBS CSI driver  
- High availability for Elasticsearch nodes  
- Secure access via NodePort and LoadBalancer services  

---

## Architecture

Kubernetes Cluster (EKS)
├─ NodeGroup1
│ └─ Pods
├─ NodeGroup2
│ └─ Pods
└─ EFK Stack
├─ Elasticsearch (StatefulSet + PVC)
├─ Fluent Bit (DaemonSet)
└─ Kibana (NodePort / LoadBalancer)

yaml
Copy code

![Architecture Diagram](screenshots/architecture-diagram.png)  <!-- Optional diagram -->

---

## Prerequisites

- AWS Account with permissions for EKS, EC2, VPC, and IAM  
- AWS CLI configured (`aws configure`)  
- `eksctl` installed  
- `kubectl` installed and configured  

---

## Setup Instructions

### 1. Create EKS Cluster

```bash
eksctl create cluster -f clusterconfig.yaml
Verify nodes:

bash
Copy code
kubectl get nodes -o wide
2. Deploy Elasticsearch
bash
Copy code
kubectl apply -f elasticsearch/
kubectl get pods -n kube-logging
kubectl get pvc -n kube-logging
3. Deploy Fluent Bit
bash
Copy code
kubectl apply -f fluent-bit/
kubectl get pods -n kube-logging
4. Deploy Kibana
bash
Copy code
kubectl apply -f kibana/
kubectl get svc -n kube-logging
Access Kibana using NodePort or LoadBalancer:

php-template
Copy code
http://<NODE_PUBLIC_IP>:<NODE_PORT>
http://<ELB_DNS>:<PORT>
5. Verify Logs
Navigate to Kibana dashboard

Check indices for logs from all pods

Create visualizations and dashboards

Useful Commands
Check all pods:

bash
Copy code
kubectl get pods -n kube-logging -o wide
Check services:

bash
Copy code
kubectl get svc -n kube-logging
Check persistent volumes:

bash
Copy code
kubectl get pvc -n kube-logging
Debug pod issues:

bash
Copy code
kubectl describe pod <pod-name> -n kube-logging
Project Outcome
Fully functional EFK stack running on EKS

Real-time centralized logging for Kubernetes workloads

Kibana dashboards for monitoring and analysis

High availability and persistent storage for Elasticsearch

References
Medium Blog: Setting up the EFK Stack

AWS EKS Documentation: https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html

Fluent Bit: https://fluentbit.io/

Elasticsearch: https://www.elastic.co/elasticsearch/

Kibana: https://www.elastic.co/kibana
