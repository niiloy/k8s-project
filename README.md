# Deploying a Multi-Tier Application on Kubernetes

This project documents the process of deploying a multi-tier MySQL and WordPress application using the Kubernetes Dashboard. It covers a range of essential Kubernetes concepts, including deployments, services, persistent volumes, secrets, and configmaps, while also integrating an NFS server for persistent data storage.

## Objective

The main objective of this project is to successfully deploy a multi-tier MySQL and WordPress application on a Kubernetes cluster. The deployment is configured with specific settings for user roles, storage, service verification, and data management.

## Technologies Used

* **Kubernetes:** An open-source container-orchestration system for automating the deployment, scaling, and management of containerized applications.
* **MySQL:** A widely-used open-source relational database management system.
* **WordPress:** A free and open-source content management system.
* **NFS (Network File System):** Used to provide a shared, persistent storage solution for the application's database and files.
* **Kubernetes Dashboard:** A web-based user interface for managing Kubernetes applications.

## Key Tasks and Steps

The following steps were performed to deploy the application:

1. **Pods, Services, and Deployments:**
   * Created the initial deployment file for MySQL (`mysql.yaml`).
   * Created the deployment file for WordPress (`wordpress.yaml`).

2. **Service Creation and Verification:**
   * Created a service file for WordPress (`wordpress-service.yaml`) to expose the application.
   * Verified the service using `kubectl describe`.

3. **Kubernetes Dashboard Configuration:**
   * Generated a token to access the Kubernetes Dashboard securely.

4. **NFS Server Setup:**
   * Configured an NFS server on a master node to manage shared storage.
   * Set up an export directory for the database and application files (`/nfsdbdata`, `/nfswpdata`).

5. **NFS Client Side Configuration:**
   * Installed and configured the `nfs-common` client on the necessary nodes to access the NFS server.

6. **Persistent Volumes (PV) and Claims (PVC):**
   * Created and applied a `PersistentVolume` (`pv.yaml`) to define the storage volume.
   * Created and applied a `PersistentVolumeClaim` (`pvc.yaml`) to request storage for the application.

7. **Secrets Management:**
   * Created a generic secret for sensitive data, such as the MySQL root password.
   * Applied the secret to the MySQL deployment.

8. **ConfigMaps for Non-Sensitive Data:**
   * Created a `ConfigMap` to store non-sensitive configuration data for the WordPress deployment.

## Project Structure

```
.
├── mysql.yaml
├── wordpress.yaml
├── wordpress-service.yaml
├── pv.yaml
├── pvc.yaml
└── README.md
```

## How to Deploy

To replicate this deployment, ensure you have a running Kubernetes cluster and an NFS server configured.

1. Place the provided YAML files (`mysql.yaml`, `wordpress.yaml`, etc.) in your working directory.

2. Apply each file using the `kubectl apply` command:

```bash
kubectl apply -f mysql.yaml
kubectl apply -f wordpress.yaml
kubectl apply -f wordpress-service.yaml
kubectl apply -f pv.yaml
kubectl apply -f pvc.yaml
```

3. Create the secret before applying the MySQL deployment:

```bash
kubectl create secret generic mysql-secret --from-literal=MYSQL_ROOT_PASSWORD='your_password'
```