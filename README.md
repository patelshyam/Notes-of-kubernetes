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

#### 3.1 External service
- External service is service which will open communication between external sources. eg. when you want to access some website through the browser you need to open external service.
#### 3.2 Internal service
- This service is used for internal communication. eg. for databases you do not want that the databse could be accessed by the outside world so you will use the database service as internal service.
#### 3.3 Ingress
- When you make your application for production you will allow the traffic come to one IP address and then you will forward the traffic to other nodes of the application that could be managed by Ingress. eg. Domain-name connected to IP of ingress and Ingress will forward the request to service node.

### 4. ConfigMap and Secreat 
- For configuration of application we use this feature. Whenever you change the configuration then you need to rebuild the project, push it to repository and need to rebuild that whole container that is not fare for the small changes like configuration. 
- For that we use external ConfigMap that contains credentials like DB_URL, Other service that used by application and connect that Config Map with pod so you can change the configuration on the go.
- Putting passowd, username, **Secreate keys** are not good if we put it in the plaintext in the ConfigMap. So for that we are using Secreate which will put all the things in the encoded format. 

### 5. Volums
- Whenever you restart the DB's container. the data you have stored in that could be vinished that is not good for any application. we are making volums. volums could be local harddrive or a remote storage(cloud storage). we give the link to that and the volums could store data in that location insted of in the container. So even if our DB's container need to be replaced then we can easily manage our data.

### 6. Deployments
- Whenever your main-app dies then you will have downtime for the application. In which the POD dies and another POD is connected to same service. here service is used as static ip address as well as loadbalancer in the application. which will forward all the requests to replica of the same app. 
- Any appication replica(eg. DB) that requires the datastored on internal or external storage that will be used by the **statefulset** which will decide which of the POD will use the storage for operations. eg. MySql, Mongo-DB and all apps will use the StatefulSet in order to make the things persistent.

## Kubernetes Architecture
### Master node
- Four processes run on every master node
	- **API Server:** Works as a cluster gateway. Initial request for updating something in the cluster comes here. It Acts as a gatekeepar for authentication!
	-  **Scheduler :** After Api server authenticate the request coming from the user the scheduler will come in action for schedul for that application. Scheduler will look for the node which will having least amount of resources used and assign the whole pod to that worker node. Actually starting of the pod is again managed by kublets.
	- **Controller Manager:** This process will detect the state change in the container like crashing of the container. If some pod dies then Controller manager send request to the scheduler and scheduler will do the same process above.
	- **etcd:** This process is the brain of the cluster all the information about which pod is running where or the process described above get all the data that needed for processing will be stored in the etcd. it is Key  valuer store. (eg. what resources available?, Did the cluster state change?, Is the cluster healthy?)
 
### Slave nodes or Worker node
- Three processes runs on the slave node.
	-  **Container runtime** (Docker)
	- **Kubelet** (This process is responsible for manage the container runtime to manage the processes between the containers. Kubelet interacts with both - the container and node. Kubelet starts the pod with a container inside.)
	- **Kube Proxy** (Kube proxy is the proxy responsible for communication between the nodes. It is intelligent enough that if the pod replica is in the same node then it could just manage to forward the same request to local replica rather that reduce the network overload. )

## Minikube
- In production envirounment there are 2 Master node and 3 Worker node. For just testing perpous it is not possiable to setup the whole envirounment. So Minikube is the application that will simulate the whole thing using virtual box. It will having master processes and worker processed, docker as a container runtime already installed.
-  There are theree ways using which the minikub can communicate with the API server 
	1. Kubernetes UI
	2. API
	3. CLI (Kubectl) (This is the most powerful tool that can do anything with the cluster)
