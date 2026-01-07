# Graded Assignment on Container Orchestration
Objective: To automate the pipeline using ECR, EKS and Jenkins and deploy the app

Github Link: https://github.com/SamDonald-A/ShopNow-Container-Orchestration 
---

# Step 1: Git and local code setup

•	Fork or Clone and Push it to your repo

<img width="975" height="477" alt="image" src="https://github.com/user-attachments/assets/2d4764ea-949c-4e07-aec5-beed6868b45f" />

•	Go to backend folder and do npm install then start the backend server to locally run the app for testing

<img width="976" height="442" alt="image" src="https://github.com/user-attachments/assets/b0272528-8504-4af0-9321-e6714626dde0" />

•	Do the same for frontend as well

<img width="976" height="460" alt="image" src="https://github.com/user-attachments/assets/c0d5444e-587d-4e5d-a468-7d2f1ac4b445" />

•	App is running locally without Docker and Kubernetes

<img width="976" height="497" alt="image" src="https://github.com/user-attachments/assets/5c60e62b-6f7f-4920-8323-6ad3203228ce" />

# Step 2: Containerization - Docker setup

•	Since we have Dockerfile Build it

<img width="976" height="480" alt="image" src="https://github.com/user-attachments/assets/969cc05a-756d-471c-98a5-cd7ef877b93e" />

•	Need to create repository for frontend and backend in DockerHub for pushing images

<img width="936" height="474" alt="image" src="https://github.com/user-attachments/assets/d8759b92-5d55-47b4-b4e2-2a309d058dde" />

<img width="936" height="453" alt="image" src="https://github.com/user-attachments/assets/df4adb3f-f382-49a3-9f11-34a41276a5da" />

<img width="936" height="240" alt="image" src="https://github.com/user-attachments/assets/92871133-c01a-48e2-b5ec-a9ecd2f6a78c" />

•	Tag each images from local

<img width="976" height="171" alt="image" src="https://github.com/user-attachments/assets/f70b2a6d-b561-4f55-a96b-657098cf8dba" />

•	Push it to DockerHub

<img width="976" height="262" alt="image" src="https://github.com/user-attachments/assets/ad331fd9-fd89-46ca-a88a-974db5c0570f" />

# Step 3: Container orchestration - Create Kubernetes manifest files

<img width="974" height="391" alt="image" src="https://github.com/user-attachments/assets/67714ee2-4e44-4e10-bec6-901ca6f61e0b" />

•	Now app is running in Minikube from Kubernetes – We can Access it via minikube tunnel

<img width="976" height="497" alt="image" src="https://github.com/user-attachments/assets/f1227148-f434-45d6-85e5-bde6310a46ec" />

# Step 4: Create Helm and EKS

•	Create Helm folder inside your project root

<img width="976" height="288" alt="image" src="https://github.com/user-attachments/assets/63b97a63-536e-42cd-8941-f1a2a1f2f3b7" />


•	Install and deploy helm to create resources – Containers and services are running now
•	Make sure your delete all the resources that are created before for testing k8s manifest files because helm will create everything fresh again.  

<img width="976" height="347" alt="image" src="https://github.com/user-attachments/assets/340da7ae-a9df-4581-8246-2a23b60d73a0" />


•	Resources are created and app deployed using helm chart

<img width="976" height="501" alt="image" src="https://github.com/user-attachments/assets/8f871ab3-7360-4313-8607-a42d11a36482" />

# Step 5: Jenkinsfile and Jenkin setup

•	Create Jenkins file

<img width="975" height="497" alt="image" src="https://github.com/user-attachments/assets/5d39dddc-ba0b-4598-9faa-c75cdb60eac6" />

•	Create Jenkins server in the EC2 and open it in the browser via IP address and login

<img width="975" height="528" alt="image" src="https://github.com/user-attachments/assets/f5abac9b-d66f-467f-919f-0a439bb45a31" />

•	Click create New Item on the top left

<img width="976" height="497" alt="image" src="https://github.com/user-attachments/assets/db84fdc7-9e57-4f7a-8c18-79965481cdce" />

•	Give name & Select Pipeline

<img width="976" height="492" alt="image" src="https://github.com/user-attachments/assets/fb250eea-6fa8-4971-9ca9-2cae7da8db89" />

•	Selcte GitHub Hook trigger for GITScm polling (We need to setup webhook in the git repo)

<img width="976" height="494" alt="image" src="https://github.com/user-attachments/assets/38c89a0b-3740-4752-bef2-367dcda40bb8" />

•	Provide that Git repo link here and select your branch

<img width="976" height="432" alt="image" src="https://github.com/user-attachments/assets/ab2ea68e-5250-4626-8e7d-1b8c20bde540" />

<img width="976" height="492" alt="image" src="https://github.com/user-attachments/assets/9f6633ac-6014-4022-be45-89d0b0a3d0ef" />


•	Setup Webhook in Github Repository – Goto settings of your repo and click webhook

<img width="976" height="492" alt="image" src="https://github.com/user-attachments/assets/227217ab-b6f6-432c-b259-7757e8d4bc9a" />

•	Click add New then add Payload and select Json

<img width="976" height="484" alt="image" src="https://github.com/user-attachments/assets/174c88a8-59dc-4e6a-ae64-3465cb6909c2" />

•	Click Add webhook

<img width="974" height="403" alt="image" src="https://github.com/user-attachments/assets/c8a2cf2b-d385-4e23-999d-49ffb413e0dd" />

Now we can push the and the Jenkin will be triggered

•	Now setup the Docker Credentials in the Jenkins Global secret

<img width="976" height="492" alt="image" src="https://github.com/user-attachments/assets/419dac12-cfc5-401e-bc75-9864243f4d56" />

•	Create EKS Cluster

<img width="975" height="452" alt="image" src="https://github.com/user-attachments/assets/969be8d9-ba0a-4fe7-a251-8b4a3c8cbf61" />

<img width="974" height="133" alt="image" src="https://github.com/user-attachments/assets/1d32ebe0-03ae-4548-85fc-6464d0fae94f" />

<img width="976" height="127" alt="image" src="https://github.com/user-attachments/assets/52d59518-022a-4492-be64-9716b048dc8b" />

# Step 6: Check Jenkins Host server requirements for EKS to run the app

Make sure all the services are installed
•	Docker
•	Helm
•	Aws CLI
•	kubectl 
•	At least t3.midium in EC2 for running the pipeline
•	At least 20gb storage for the npm and other installation process on the machine
•	EKS IAM Role permissions
•	Jenkins
•	Jenkins credentials
•	Jenkins plugins
•	eksctl

<img width="975" height="154" alt="image" src="https://github.com/user-attachments/assets/8de5f051-71c7-48d3-9e5a-d0331ce7a8a9" />


•	Also make sure all required plugins installed in Jenkins

<img width="975" height="243" alt="image" src="https://github.com/user-attachments/assets/b777cf20-a287-4da5-8b93-e414aba1da23" />

•	Then Change the Jenkins pipeline flow according to your requirements and push the code to the repository

<img width="976" height="293" alt="image" src="https://github.com/user-attachments/assets/14d134a0-5b6b-47e2-b43a-edf47b8ad874" />

•	Pipeline triggered

<img width="976" height="503" alt="image" src="https://github.com/user-attachments/assets/b536e972-9555-4b5a-ae15-6db3c557bd57" />

•	Study the log on the pipeline failure and Fix

<img width="976" height="485" alt="image" src="https://github.com/user-attachments/assets/64248fa9-1538-4591-a006-9cf982243668" />

•	Make sure you have this role in your EC2 IAM of Jenkins Server

<img width="976" height="424" alt="image" src="https://github.com/user-attachments/assets/45737ad6-1235-4ee7-8153-8864d82f4c03" />

 •	After debuging, push the code and check the pipeline then Check All Pods and services are running on the success


# 🛒 ShopNow E-Commerce - Kubernetes Learning Project

ShopNow is a **Kubernetes learning project** built around a full-stack MERN e-commerce application:
- **Customer App** (React frontend)  
- **Admin Dashboard** (React admin panel)  
- **Backend API** (Express + MongoDB)  

This project teaches **Kubernetes** from container basics to production-ready deployments with Dockerfiles, Kubernetes manifests, Helm, GitOps and CICD using Jenkins.

## 🎯 Learning Objectives
- Write Dockerfiles for containerising the application
- Master Kubernetes fundamentals through hands-on practice
- Understand and implement HELM Chart for application deployment on kubernetes
- Implement GitOps workflows using ArgoCD
- Implement CICD pipelines using Jenkins

---

## 📁 Project Structure

```
shopNow/
├── backend/               # Node.js API server
├── frontend/              # React customer app
├── admin/                 # React admin dashboard
├── kubernetes
│   ├── k8s-manifests/     # Raw Kubernetes YAML files
│   ├── helm/              # Helm charts for package management
│   │   └── charts/        # Individual charts
│   ├── argocd/            # GitOps deployment configs
│   └── pre-req/           # Cluster prerequisites
├── jenkins/               # Pipeline definitions (CI & CD)       
├── docs/                  # learning resources and guides
└── scripts/               # Automation and utility scripts
```

---

## 🚀 Learning Journey

### Container & Kubernetes Basics
1. **Start Here**: [docs/K8S-CONCEPTS.md](docs/K8S-CONCEPTS.md) - Core concepts explained
2. **Raw Kubernetes Manifests**: `kubernetes/k8s-manifests/`

### Package Management & Automation  
3. **Helm Charts**: `kubernetes/helm/`
4. **CI/CD Pipelines**: `jenkins/`

### GitOps & Production Readiness
5. **ArgoCD GitOps**: `kubernetes/argocd/`


## Getting Started

## 🛠 Prerequisites & Setup

#### 1. Setup Tools**: [docs/TOOLS-SETUP-GUIDE.md](docs/TOOLS-SETUP-GUIDE.md)

#### 2. AWS ECR Registry Setup 
```bash
# Setup AWS credentials first
aws configure
# Enter your AWS Access Key ID, Secret Access Key, region (us-east-1), and output format (json)

# Or use environment variables
export AWS_ACCESS_KEY_ID=your-access-key
export AWS_SECRET_ACCESS_KEY=your-secret-key
export AWS_DEFAULT_REGION=us-east-1

# If above credentials are already set, run below command to verify
aws sts get-caller-identity

# Create ECR repositories either via the aws cli as mentioned below or via console (Has to be done once to create the ECR repo, skip this step when you are rebuilding the docker images):

like:

aws ecr create-repository --repository-name <your-username>-shopnow/frontend --region <region>
aws ecr create-repository --repository-name <your-username>-shopnow/backend --region <region>
aws ecr create-repository --repository-name <your-username>-shopnow/admin --region <region>

# Get login token (run this command everytime as the docker credentials are persisted only on the terminal)
aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <account-id>.dkr.ecr.<region>.amazonaws.com
```


#### 3. Update Configurations in below mentioned files


## 🔧 Personalization Required

**For Multi-User Kubernetes Clusters**: To avoid conflicts when multiple learners use the same cluster, each user must personalize their deployment with unique identifiers.

**IMPORTANT**: This project contains hardcoded references that you must update with your own values:

3.1. Replace "aryan" with your username in these locations:

  **Ingress Paths** (in both Kubernetes manifests and Helm charts):
   - `kubernetes/k8s-manifests/ingress/ingress-shopnow.yaml`
     - Change `/aryan` to `/<your-username>`
     - Change `/aryan-admin` to `/<your-username>-admin`
   
   - `kubernetes/helm/charts/frontend/values.yaml`
     - Change `path: /aryan` to `path: /<your-username>`
   
   - `kubernetes/helm/charts/admin/values.yaml`
     - Change `path: /aryan-admin` to `path: /<your-username>-admin`


  **Nginx ConfigMaps**
   - All references with 'aryan' to <your-username> in following files:
   - `kubernetes/k8s-manifests/frontend/cm-nginx.yaml`   
   - `kubernetes/k8s-manifests/admin/cm-nginx.yaml`


  **Helm Chart Nginx Configurations**:
   - All references with 'aryan' in the 'nginx.config' section to <your-username> in following files:
   - `kubernetes/helm/charts/frontend/values.yaml` 
   - `kubernetes/helm/charts/admin/values.yaml`

  **Dockerfiles** (Build Arguments):
   - `frontend/Dockerfile`
     - Change `ARG USER_NAME=aryan` to `ARG USER_NAME=<your-username>`
   
   - `admin/Dockerfile`
     - Change `ARG USER_NAME=aryan` to `ARG USER_NAME=<your-username>`

  **Build Script** (optional):
   - `scripts/build-and-push.sh`
     - Update the example usage comments that reference "aryan"

3.2. **ECR Repository Names** - Update to your username:
   - All `kubernetes/k8s-manifests/*/deployment.yaml` files
   - All `kubernetes/helm/charts/*/values.yaml` files
   - All `jenkins\Jenkinsfile.*.*` files
   - Change `shopnow/frontend` to `<your-username>-shopnow/frontend`
   - Change `shopnow/backend` to `<your-username>-shopnow/backend`
   - Change `shopnow/admin` to `<your-username>-shopnow/admin`

3.3. **Update Namespace** on these locations:
  - `kubernetes/k8s-manifests/namespace/namespace.yaml` - Change namespace name
  - All files in `kubernetes/k8s-manifests/*/` - Update namespace references
  - `kubernetes/argocd/apps/*.yaml` - Update destination namespace
  - All kubectl commands in this README - Replace `shopnow-demo` with your namespace

3.4. **Update ArgoCD Repository URL**:
  - In `kubernetes/argocd/umbrella-application.yaml` and all `kubernetes/argocd/apps/*.yaml` files:
  - Change `repoURL: 'https://github.com/aryanm12/shopNow'` 
  - To `repoURL: 'https://github.com/<your-github-username>/<your-repo-name>'`



#### 4. Kubernetes Cluster Access (Make sure to have a running Kubernetes cluster, here is an example to connect with EKS)
```bash
# For EKS cluster
aws eks update-kubeconfig --region <region> --name <your-cluster-name>

# Verify access
kubectl cluster-info
kubectl get nodes
```

Note: All the below mentioned kubectl commands assume that you are working with "shopnow-demo" namespace, update the namespace as per yours where ever you find "shopnow-demo".

#### 5. Docker Registry Secret (Only required for private ECR registry)
**Note**: Skip this step if using public Docker Hub images or public ECR repositories.

```bash
# Create registry secret for private ECR image pulls
kubectl create ns shopnow-demo
kubectl create secret docker-registry ecr-secret --docker-server=<account-id>.dkr.ecr.us-east-1.amazonaws.com --docker-username=AWS --docker-password=$(aws ecr get-login-password --region us-east-1) --namespace=shopnow-demo
```

#### 6. Install Pre-requisites in the Kubernetes Environment (Has to be done once per Kubernetes Cluster)
```bash
# Install metrics server (required for resource monitoring and HPA)
kubectl apply -f kubernetes/pre-req/metrics-server.yaml

# Install ingress-nginx controller (for external access)
# For EKS, other cloud provider will have different file
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.12.0-beta.0/deploy/static/provider/aws/deploy.yaml

# For local development (minikube/kind/Docker Desktop)
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.1/deploy/static/provider/kind/deploy.yaml

# Verify installations
kubectl get pods -n kube-system
kubectl get pods -n ingress-nginx
kubectl top nodes  # Should work after metrics server is running
kubectl top pods  # Should work after metrics server is running

# To enable Persistent Storage

# First install the EBS CSI driver as an EKS Addon

-> In the EKS Console, open your cluster → go to Add-ons → click Get more add-ons → select Amazon EBS CSI driver → click Next.
-> On the configuration page, Under Pod identity association, choose Create a new IAM role, and the console will auto-attach the AmazonEBSCSIDriverPolicy.
-> Confirm and click Create. The add-on installs, the IAM role is associated with the SA via Pod Identity, and the driver starts running.
-> Verify under Add-ons tab that the EBS CSI driver is active and under Pod identity associations tab you see the SA <-> IAM role mapping.

# Install storage class for persistent volumes
kubectl apply -f kubernetes/pre-req/storageclass-gp3.yaml

# Verify storage class installation
kubectl get storageclass


```


## ⚡ Build and Deploy the micro-services

### 1. Build the docker images and push it to the ECR registry created above

```bash
scripts/build-and-push.sh <account-id>.dkr.ecr.<region>.amazonaws.com/<registry-name> <tag-name-number> <your-username> 

# Example for user 'aryan' with tag 'latest' and ECR registry '975050024946.dkr.ecr.ap-southeast-1.amazonaws.com/shopnow':
./scripts/build-and-push.sh 975050024946.dkr.ecr.ap-southeast-1.amazonaws.com/shopnow latest aryan


```

### 2. Choose Your Deployment Method

**Option A: Raw Kubernetes Manifests**
```bash
kubectl apply -f kubernetes/k8s-manifests/namespace/
kubectl apply -f kubernetes/k8s-manifests/database/
kubectl apply -f kubernetes/k8s-manifests/backend/
kubectl apply -f kubernetes/k8s-manifests/frontend/
kubectl apply -f kubernetes/k8s-manifests/admin/
kubectl apply -f kubernetes/k8s-manifests/ingress/
kubectl apply -f kubernetes/k8s-manifests/daemonsets-example/
```

**Option B: Helm Charts**

```bash
helm upgrade --install mongo kubernetes/helm/charts/mongo -n shopnow-demo --create-namespace
helm upgrade --install backend kubernetes/helm/charts/backend -n shopnow-demo
helm upgrade --install frontend kubernetes/helm/charts/frontend -n shopnow-demo
helm upgrade --install admin kubernetes/helm/charts/admin -n shopnow-demo
```

**Option C: ArgoCD GitOps**
```bash
# Install ArgoCD first
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Create target namespace
kubectl create namespace shopnow-demo

# Deploy applications
kubectl apply -f kubernetes/argocd/umbrella-application.yaml

# Check all ArgoCD application status:
kubectl get applications -n argocd

```

### 3. Create users in MongoDB after the mongodb pods are healthy

```bash

# check the status of the mongo-0 pods 
kubectl get pods -n shopnow-demo

# if mongo-0 pod is healthy, then run following command to create a user for the backend to connect
# user credentials should be same as mentioned in the backend secrets-db.yaml file
# First exex into the pods
kubectl -n shopnow-demo exec -it mongo-0 -- mongosh

# Run below commands
use admin;
db.createUser({
  user: 'shopuser',
  pwd: 'ShopNowPass123',
  roles: [
    { role: 'readWrite', db: 'shopnow' },
    { role: 'dbAdmin', db: 'shopnow' }
  ]
});

exit

# Restart backend deployment
kubectl rollout restart deploy backend -n shopnow-demo
```

### 3. Check the resources deployed

```bash
# Check Pods
kubectl get pods -n shopnow-demo

# Check Deployment
kubectl get deploy -n shopnow-demo

# Check Services
kubectl get svc -n shopnow-demo

# Check daemonsets
kubectl get daemonsets -n shopnow-demo

# Check statefulsets
kubectl get statefulsets -n shopnow-demo

# Check HPA
kubectl get hpa -n shopnow-demo

# Check all of the above at once
kubectl get all -n shopnow-demo

# Check configmaps
kubectl get cm -n shopnow-demo

# Check secrets
kubectl get secrets -n shopnow-demo

# Check ingress
kubectl get ing -n shopnow-demo

# Sequence to debug in case of any issue with the pods
kubectl get pods -n shopnow-demo
kubectl describe pod backend-746cc99cd-cqrgf -n shopnow-demo # Assuming that pod backend-746cc99cd-cqrgf has an error
kubectl logs backend-746cc99cd-cqrgf -n shopnow-demo --previous # If no details are found in the above command or if details like liveness probe failed are coming

```


---

## 🌐 Access the Apps

* **Customer App** → [http://<load-balancer-ip-or-dns>/<your-username>](http://<load-balancer-ip-or-dns>/<your-username>)
* **Admin Dashboard** → [http://<load-balancer-ip-or-dns>/<your-username>-admin](http://<load-balancer-ip-or-dns>/<your-username>-admin)

---

## Additional Notes

**Check the Application Architecture details**: [docs/APPLICATION-ARCHITECTURE.md](docs/APPLICATION-ARCHITECTURE.md)
**Check the Troubleshooting Guide**: [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md)
---

## 👨‍💻 Author

## K Mohan Krishna

---

