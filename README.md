# MySQL on Kubernetes 🗄️

A production-style MySQL deployment on Kubernetes using Docker Desktop.
Built to learn and demonstrate core Kubernetes and DevOps concepts.

## 🛠️ Tech Stack
- Kubernetes (Docker Desktop)
- MySQL 8.0
- kubectl
- Git

## 📚 Concepts Covered
- Kubernetes Secrets (managing sensitive credentials securely)
- PersistentVolume & PersistentVolumeClaim (dynamic storage provisioning)
- Kubernetes Deployments (running and managing containers)
- Kubernetes Services (stable networking with ClusterIP)
- kubectl (interacting with the cluster)
- Git workflow (incremental commits, .gitignore)

## 📁 Project Structure
```
mysql-on-kubernetes/
├── k8s/
│   ├── secret.yaml        # MySQL credentials (base64 encoded)
│   ├── storage.yaml       # PersistentVolumeClaim for MySQL data
│   ├── deployment.yaml    # MySQL 8.0 Deployment with resource limits
│   └── service.yaml       # ClusterIP Service on port 3306
└── README.md
```

## 🚀 How to Run Locally

### Prerequisites
- Docker Desktop with Kubernetes enabled
- kubectl installed
- Git installed

### Steps

1. Clone the repo
   git clone https://github.com/subhojit07Das/my-sql-k8s.git
   cd mysql-on-kubernetes

2. Create your own secrets
   echo -n "yourpassword" | base64

   Update k8s/secret.yaml with your own base64 encoded values.

3. Deploy everything
   kubectl apply -f k8s/secret.yaml
   kubectl apply -f k8s/storage.yaml
   kubectl apply -f k8s/deployment.yaml
   kubectl apply -f k8s/service.yaml

4. Verify everything is running
   kubectl get pods
   kubectl get pv
   kubectl get pvc
   kubectl get svc

5. Connect to MySQL
   kubectl exec -it <pod-name> -- mysql -u root -p

6. Test persistence

   Delete the pod:
```bash
   kubectl delete pod 
```
   Watch Kubernetes recreate it automatically:
```bash
   kubectl get pods -w
```
   Connect to the new pod:
```bash
   kubectl exec -it <pod_name> -- mysql -u root -p
```
   Your data is still there! ✅

## 💡 Key Learnings

**Kubernetes Secrets** store sensitive data separately from app config.
Never hardcode passwords in YAML files!

**Dynamic Provisioning** lets Kubernetes automatically create
PersistentVolumes when a PVC is applied — same way GKE works in production!

**ClusterIP Service** gives MySQL a stable internal IP so other apps
can connect to it reliably even when pods restart and get new IPs.

**Infrastructure as Code** — entire infrastructure defined in YAML files.
One command to bring everything up, one command to tear it down.

## 🔮 Next Steps
- [ ] Deploy to GKE (Google Kubernetes Engine)
- [ ] Add a web app that connects to this MySQL instance
- [ ] Set up CI/CD pipeline with GitHub Actions
- [ ] Add Horizontal Pod Autoscaling

## 📄 Resume Description
Deployed a production-style MySQL 8.0 instance on Kubernetes using Docker Desktop. 
Implemented secure credential management with K8s Secrets, dynamic persistent 
storage with PVC, and stable networking with ClusterIP Services. Managed full 
deployment lifecycle using kubectl and Git.

## 👨‍💻 Author
Subhojit Das
GitHub: https://github.com/subhojit07Das