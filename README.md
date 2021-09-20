# Notes of kubernetes

## What is Kubernetes?
- Kubernetes is an open-source container-orchestration system for automating computer application deployment, scaling, and management.
- Because of trend from Monolitch to Microservice architecture It is necessary to have a tool to manage all mircoservice at oneplatform.
-  Some application use thousands of application In which it is impossiable or very hard to manage those manually or by scripts.

## Features of Kubernetes
- High availability or no downtime.
- Scalability or high performance
- Disaster recovery - backup and restore

## Fundamental concepts of Kubernetes. (Need to know before developing)
- Node (Worker node)
- Pod

### 1. Node (Worker node)
- Worker node is the virtual machine or physical machine
- Node could have multiple pods.

### 2. Pod (Smallest unit of K8s)
- Pod is the smallest unit of the kubernetes.
- Pod creates the running envirounment for containers.
- Pod usually build to run one container inside them.
- One node can have multiple pods.
- Each pod have their own IP address, using which pods communicate with each other.
- New ip address on re-creation.

### 3. Service
- Recreation of the pod can lead to new IP address which is not good if the application communicates using the IP address
- So each pod also having permanent IP address or static IP address which is known as Static IP address.
- Lifecycle of Pod and Service NOT connected so even if pod dies service stays there
