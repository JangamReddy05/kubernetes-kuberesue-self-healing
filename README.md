# 🚀 KubeRescue — Kubernetes Autonomous Self-Healing & Fault Recovery Platform

KubeRescue is a Kubernetes-based **self-healing and fault-recovery platform** designed to demonstrate how Kubernetes can automatically detect failures, maintain application availability, recover workloads, preserve persistent data, and safely recover from failed deployments.

The project intentionally introduces different failure scenarios and validates Kubernetes-native recovery mechanisms such as **Deployments, ReplicaSets, Liveness Probes, Readiness Probes, HPA, PDB, PV/PVC, ConfigMaps, Secrets, NetworkPolicies, Rolling Updates, Rollbacks, Node Affinity, Taints, and Tolerations**.

---

## 📌 Project Overview

In a production Kubernetes environment, applications can fail because of:

* Pod crashes
* Container failures
* Bad application deployments
* Resource exhaustion
* Configuration errors
* Scheduling problems
* Network access violations
* Pod disruptions
* Application restarts

KubeRescue simulates these situations and demonstrates how Kubernetes responds and recovers.

### Core idea

```text
                    Kubernetes Cluster
                           │
                       Ingress
                           │
                       Service
                           │
             ┌─────────────┼─────────────┐
             │             │             │
           Pod-1         Pod-2         Pod-3
             │             │             │
             └─────────────┼─────────────┘
                           │
                    Health Probes
                    ┌──────┴──────┐
                    │             │
                Liveness      Readiness
                    │             │
                    └──────┬──────┘
                           │
                    Recovery Layer
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   Pod Recovery        Deployment         Resource
                       Rollback            Scaling
        │                  │                  │
        └──────────────────┼──────────────────┘
                           │
                    Kubernetes Recovery
```

---

# 🎯 Project Objectives

The main objectives of KubeRescue are:

* Demonstrate Kubernetes self-healing capabilities.
* Automatically replace failed Pods.
* Detect unhealthy containers using health probes.
* Control traffic using readiness probes.
* Demonstrate rolling updates and rollback.
* Preserve application data using persistent storage.
* Secure workloads using Secrets and NetworkPolicies.
* Demonstrate Kubernetes scheduling mechanisms.
* Maintain application availability using PodDisruptionBudgets.
* Demonstrate automatic scaling using HPA.
* Document and reproduce real Kubernetes failure scenarios.

---

# 🛠️ Technologies Used

| Technology                | Purpose                         |
| ------------------------- | ------------------------------- |
| Kubernetes                | Container orchestration         |
| kubectl                   | Kubernetes cluster management   |
| Docker Desktop Kubernetes | Local Kubernetes cluster        |
| YAML                      | Kubernetes resource definitions |
| Git                       | Version control                 |
| GitHub                    | Source code and documentation   |
| NGINX                     | Sample application              |

### Kubernetes Concepts

* Pods
* Deployments
* ReplicaSets
* Services
* Namespaces
* Liveness Probes
* Readiness Probes
* ConfigMaps
* Secrets
* Resource Requests & Limits
* Horizontal Pod Autoscaler
* PersistentVolumes
* PersistentVolumeClaims
* NetworkPolicies
* Node Affinity
* Taints & Tolerations
* PodDisruptionBudgets
* Rolling Updates
* Rollbacks

---

# 🏗️ Architecture

```text
                         KUBERESCUE
                             │
                     Kubernetes Cluster
                             │
                        ┌────▼────┐
                        │ Service │
                        └────┬────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
           ┌──▼──┐        ┌──▼──┐        ┌──▼──┐
           │Pod 1│        │Pod 2│        │Pod 3│
           └──┬──┘        └──┬──┘        └──┬──┘
              │              │              │
              └──────────────┼──────────────┘
                             │
                    ┌────────▼────────┐
                    │ Health Probes   │
                    └────────┬────────┘
                             │
             ┌───────────────┼────────────────┐
             │               │                │
         Liveness         Readiness           HPA
             │               │                │
             └───────────────┼────────────────┘
                             │
                      Recovery Layer
                             │
      ┌──────────────────────┼─────────────────────┐
      │                      │                     │
   Rollback               Storage              Security
      │                      │                     │
 Rolling Update           PV / PVC         Secret / NetworkPolicy
                             │
                      Scheduling Layer
                             │
                Affinity / Taints / Tolerations
                             │
                        PDB / Availability
```

---

# 📁 Project Structure

```text
kubernetes-kuberescue/
│
├── README.md
│
├── namespace/
│   └── kuberesue-namespace.yaml
│
├── application/
│   ├── deployment.yaml
│   ├── service.yaml
│   └── configmap.yaml
│
├── health-checks/
│   ├── liveness.yaml
│   └── readiness.yaml
│
├── resources/
│   ├── resource-limits.yaml
│   └── hpa.yaml
│
├── storage/
│   ├── pv.yaml
│   ├── pvc.yaml
│   └── deployment-storage.yaml
│
├── security/
│   ├── secret.yaml
│   └── networkpolicy.yaml
│
├── scheduling/
│   ├── node-affinity.yaml
│   ├── taint.yaml
│   └── toleration.yaml
│
├── availability/
│   └── pdb.yaml
│
├── rolling-updates/
│   ├── deployment-v1.yaml
│   └── deployment-v2.yaml
│
├── failure-tests/
│   ├── 01-pod-failure.md
│   ├── 02-container-failure.md
│   ├── 03-bad-deployment.md
│   ├── 04-rollback.md
│   ├── 05-storage-recovery.md
│   ├── 06-network-failure.md
│   ├── 07-resource-stress.md
│   └── 08-scheduling-failure.md
│
├── docs/
│   ├── kuberesue-architecture.png
│   ├── failure-scenarios.md
│   └── troubleshooting.md
│
└── screenshots/
    ├── 01-github-repository.png
    ├── 02-git-clone.png
    ├── 03-kubernetes-cluster.png
    ├── 04-namespace.png
    ├── 05-three-replicas.png
    ├── 06-application-running.png
    ├── 07-liveness-probe.png
    ├── 08-health-checks.png
    ├── 09-pod-self-healing.png
    ├── 10-rolling-update.png
    ├── 11-deployment-failure.png
    ├── 12-successful-rollback.png
    ├── 13-persistent-storage.png
    ├── 14-network-policy.png
    ├── 15-scheduling.png
    ├── 16-pdb.png
    ├── 17-hpa-scaling.png
    └── 18-architecture.png
```

---

# 🚀 Installation & Setup

## 1. Prerequisites

Install the following:

* Docker Desktop
* Kubernetes
* kubectl
* Git
* GitHub account

Verify the installations:

```bash
docker --version
kubectl version --client
git --version
```

Verify Kubernetes:

```bash
kubectl cluster-info
```

Check nodes:

```bash
kubectl get nodes
```

Expected:

```text
NAME             STATUS   ROLES           AGE
docker-desktop   Ready    control-plane   ...
```

---

# 2. Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/kubernetes-kuberescue.git
```

Navigate into the project:

```bash
cd kubernetes-kuberescue
```

---

# 3. Create Kubernetes Namespace

```bash
kubectl apply -f namespace/kuberesue-namespace.yaml
```

Verify:

```bash
kubectl get namespace kuberesue
```

Expected:

```text
NAME         STATUS
kuberesue    Active
```

---

# 4. Deploy the Application

Apply the Deployment:

```bash
kubectl apply -f application/deployment.yaml
```

Verify:

```bash
kubectl get deployment -n kuberesue
```

Check Pods:

```bash
kubectl get pods -n kuberesue
```

The application should run with multiple replicas.

---

# 5. Create the Service

```bash
kubectl apply -f application/service.yaml
```

Verify:

```bash
kubectl get svc -n kuberesue
```

---

# 6. Access the Application

Use port forwarding:

```bash
kubectl port-forward svc/kuberesue-service 8080:80 -n kuberesue
```

Open:

```text
http://localhost:8080
```

---

# ❤️ Self-Healing Demonstration

One of the primary objectives of KubeRescue is demonstrating Kubernetes self-healing.

First check the Pods:

```bash
kubectl get pods -n kuberesue
```

Delete one Pod:

```bash
kubectl delete pod <pod-name> -n kuberesue
```

Watch the Pods:

```bash
kubectl get pods -n kuberesue -w
```

### Expected behavior

```text
Pod deleted
     ↓
Replica count decreases
     ↓
ReplicaSet detects missing replica
     ↓
New Pod created
     ↓
New Pod becomes Ready
     ↓
Desired replica count restored
```

### Evidence

![Pod Self Healing](screenshots/09-pod-self-healing.png)

---

# ❤️‍🩹 Liveness Probe

The liveness probe checks whether the application container is healthy.

Example:

```yaml
livenessProbe:
  httpGet:
    path: /
    port: 80
  initialDelaySeconds: 10
  periodSeconds: 5
  failureThreshold: 3
```

If the container repeatedly fails its liveness probe, Kubernetes can restart the container.

Verify:

```bash
kubectl describe pod <pod-name> -n kuberesue
```

### Evidence

![Liveness Probe](screenshots/07-liveness-probe.png)

---

# 🚦 Readiness Probe

The readiness probe determines whether a Pod should receive application traffic.

Example:

```yaml
readinessProbe:
  httpGet:
    path: /
    port: 80
  initialDelaySeconds: 5
  periodSeconds: 5
```

When the readiness check fails, the Pod can remain running while being removed from Service traffic.

### Evidence

![Health Checks](screenshots/08-health-checks.png)

---

# 🔄 Rolling Updates

KubeRescue demonstrates controlled application updates.

Check rollout status:

```bash
kubectl rollout status deployment/kuberesue-app -n kuberesue
```

Check rollout history:

```bash
kubectl rollout history deployment/kuberesue-app -n kuberesue
```

A new application version can be deployed without immediately destroying all existing replicas.

### Evidence

![Rolling Update](screenshots/10-rolling-update.png)

---

# 💥 Failed Deployment & Recovery

A deliberately invalid container image is used to simulate a deployment failure.

Example:

```yaml
image: nginx:this-image-does-not-exist
```

Apply:

```bash
kubectl apply -f application/deployment.yaml
```

Check:

```bash
kubectl get pods -n kuberesue
```

Possible status:

```text
ImagePullBackOff
```

Investigate:

```bash
kubectl describe pod <pod-name> -n kuberesue
```

### Evidence

![Deployment Failure](screenshots/11-deployment-failure.png)

---

# 🔙 Rollback

Recover from the failed deployment:

```bash
kubectl rollout undo deployment/kuberesue-app -n kuberesue
```

Verify:

```bash
kubectl rollout status deployment/kuberesue-app -n kuberesue
```

Check Pods:

```bash
kubectl get pods -n kuberesue
```

### Expected result

The application returns to the previously working version.

### Evidence

![Successful Rollback](screenshots/12-successful-rollback.png)

---

# 💾 Persistent Storage

KubeRescue demonstrates application data persistence using Kubernetes storage.

Architecture:

```text
Application
     │
     ▼
    PVC
     │
     ▼
    PV
     │
     ▼
Persistent Data
```

The recovery test:

```text
Write Data
    ↓
Delete Application Pod
    ↓
Kubernetes Creates Replacement Pod
    ↓
Replacement Pod Mounts Same PVC
    ↓
Data Remains Available
```

Verify:

```bash
kubectl get pv
kubectl get pvc -n kuberesue
```

### Evidence

![Persistent Storage](screenshots/13-persistent-storage.png)

---

# 🔐 Kubernetes Secrets

Secrets are used for sensitive application configuration.

Example:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: kuberesue-secret
  namespace: kuberesue
type: Opaque
stringData:
  APP_USERNAME: demo-user
  APP_PASSWORD: demo-password
```

> ⚠️ Only demonstration credentials are used in this repository. Never commit real passwords, API keys, tokens, certificates, or cloud credentials to GitHub.

---

# ⚙️ ConfigMap

ConfigMaps provide non-sensitive application configuration.

Example:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: kuberesue-config
  namespace: kuberesue
data:
  APP_NAME: "KubeRescue"
  ENVIRONMENT: "production"
  APP_VERSION: "1.0"
```

---

# 🛡️ NetworkPolicy

KubeRescue uses Kubernetes NetworkPolicies to demonstrate network isolation.

Example architecture:

```text
Frontend
   │
   ├──────────────► Backend
   │                   │
   │                   ▼
   │                Database
   │
   └──────────X──────► Database
             Blocked
```

Verify:

```bash
kubectl get networkpolicy -n kuberesue
```

### Evidence

![Network Policy](screenshots/14-network-policy.png)

---

# 📊 Resource Management & HPA

Resource requests and limits are configured for workloads.

Example:

```yaml
resources:
  requests:
    cpu: "100m"
    memory: "128Mi"
  limits:
    cpu: "500m"
    memory: "256Mi"
```

Horizontal Pod Autoscaler can then scale the application based on resource utilization.

Example:

```text
Low CPU
   ↓
3 Pods

High CPU
   ↓
4 Pods
   ↓
5 Pods
   ↓
6 Pods
```

Check:

```bash
kubectl get hpa -n kuberesue
```

### Evidence

![HPA Scaling](screenshots/17-hpa-scaling.png)

---

# 🧭 Scheduling

The project demonstrates Kubernetes scheduling features including:

### Node Affinity

Controls which nodes can run specific workloads.

### Taints

Prevent normal Pods from being scheduled onto specific nodes.

### Tolerations

Allow selected Pods to run on tainted nodes.

Check:

```bash
kubectl get nodes --show-labels
```

Check Pod placement:

```bash
kubectl get pods -n kuberesue -o wide
```

### Evidence

![Scheduling](screenshots/15-scheduling.png)

---

# 🛡️ PodDisruptionBudget

A PodDisruptionBudget is configured to help maintain application availability during voluntary disruptions.

Example:

```yaml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: kuberesue-pdb
  namespace: kuberesue
spec:
  minAvailable: 2
  selector:
    matchLabels:
      app: kuberesue
```

Check:

```bash
kubectl get pdb -n kuberesue
```

Detailed information:

```bash
kubectl describe pdb kuberesue-pdb -n kuberesue
```

### Evidence

![PDB](screenshots/16-pdb.png)

---

# 🧪 Failure Scenarios

KubeRescue intentionally tests multiple Kubernetes failure conditions.

| Failure Scenario         | Kubernetes Mechanism    | Expected Recovery        |
| ------------------------ | ----------------------- | ------------------------ |
| Pod deleted              | Deployment / ReplicaSet | Replacement Pod          |
| Container unhealthy      | Liveness Probe          | Container restart        |
| Pod not ready            | Readiness Probe         | Traffic removed          |
| Bad image                | Deployment              | Detect failure           |
| Failed release           | Rollout                 | Rollback                 |
| High resource usage      | HPA                     | Additional replicas      |
| Pod disruption           | PDB                     | Availability protection  |
| Scheduling restriction   | Affinity                | Controlled placement     |
| Tainted node             | Toleration              | Allowed scheduling       |
| Data loss simulation     | PV/PVC                  | Persistent data          |
| Unauthorized traffic     | NetworkPolicy           | Traffic blocked          |
| Configuration change     | ConfigMap               | Controlled configuration |
| Credential configuration | Secret                  | Sensitive configuration  |

---

# 📸 Project Evidence

Screenshots are included to demonstrate actual Kubernetes behavior.

## GitHub Repository

![GitHub Repository](screenshots/01-github-repository.png)

## Kubernetes Cluster

![Kubernetes Cluster](screenshots/03-kubernetes-cluster.png)

## Three Application Replicas

![Three Replicas](screenshots/05-three-replicas.png)

## Application Running

![Application](screenshots/06-application-running.png)

## Self-Healing

![Self Healing](screenshots/09-pod-self-healing.png)

## Failed Deployment

![Deployment Failure](screenshots/11-deployment-failure.png)

## Rollback

![Rollback](screenshots/12-successful-rollback.png)

## Architecture

![Architecture](screenshots/18-architecture.png)

---

# 🧰 Troubleshooting

## Check all resources

```bash
kubectl get all -n kuberesue
```

## Check Pods

```bash
kubectl get pods -n kuberesue
```

## Detailed Pod information

```bash
kubectl describe pod <pod-name> -n kuberesue
```

## View application logs

```bash
kubectl logs <pod-name> -n kuberesue
```

## Check Deployment

```bash
kubectl describe deployment kuberesue-app -n kuberesue
```

## Check ReplicaSets

```bash
kubectl get replicasets -n kuberesue
```

## Check events

```bash
kubectl get events -n kuberesue --sort-by=.lastTimestamp
```

## Check services

```bash
kubectl get svc -n kuberesue
```

## Check storage

```bash
kubectl get pv
kubectl get pvc -n kuberesue
```

---

# 📚 Key Kubernetes Concepts Demonstrated

Through this project, the following Kubernetes concepts are practiced:

* Kubernetes Architecture
* Namespaces
* Pods
* Deployments
* ReplicaSets
* Services
* Container lifecycle
* Liveness Probes
* Readiness Probes
* Resource Requests
* Resource Limits
* Horizontal Pod Autoscaling
* ConfigMaps
* Secrets
* PersistentVolumes
* PersistentVolumeClaims
* NetworkPolicies
* Node Affinity
* Taints
* Tolerations
* PodDisruptionBudgets
* Rolling Updates
* Rollbacks
* Kubernetes Scheduling
* Failure Diagnosis
* Self-Healing

---

# 🎓 What I Learned

This project helped me understand how Kubernetes behaves during real-world failure scenarios rather than only learning Kubernetes resource definitions.

### Key learnings

* How Deployments maintain the desired replica count.
* How ReplicaSets replace failed Pods.
* How liveness probes trigger container recovery.
* How readiness probes control application traffic.
* How rolling updates work.
* How failed deployments can be rolled back.
* How Kubernetes scheduling decisions are made.
* How taints and tolerations affect scheduling.
* How affinity controls workload placement.
* How PVCs preserve application data.
* How NetworkPolicies restrict network communication.
* How PDBs help maintain availability during voluntary disruptions.
* How HPA dynamically adjusts application replicas.
* How to troubleshoot Kubernetes workloads using `kubectl`.

---

# 🏆 Project Highlights

### Self-Healing

```text
Pod Failure
     ↓
ReplicaSet Detection
     ↓
New Pod
     ↓
Application Recovery
```

### Deployment Recovery

```text
New Version
     ↓
Deployment Failure
     ↓
Failure Detection
     ↓
Rollback
     ↓
Healthy Version
```

### Persistent Data Recovery

```text
Pod Failure
     ↓
Replacement Pod
     ↓
Same PVC
     ↓
Data Preserved
```

### Resource Scaling

```text
Resource Usage Increases
          ↓
         HPA
          ↓
More Replicas
          ↓
Improved Capacity
```

---

# 🔮 Future Improvements

Potential future enhancements include:

* Multi-node Kubernetes cluster testing.
* Multi-zone high availability simulation.
* Advanced NetworkPolicy scenarios.
* Stateful application recovery.
* Automated failure testing.
* Chaos engineering experiments.
* Kubernetes admission policies.
* Pod Security Standards.
* Advanced scheduling strategies.
* Automated disaster recovery workflows.

---

# 📌 Resume Description

**KubeRescue — Kubernetes Autonomous Self-Healing & Fault Recovery Platform**

* Designed and implemented a Kubernetes-based self-healing platform using Deployments, ReplicaSets, Services, health probes, HPA, PDB, ConfigMaps, Secrets, PV/PVC, NetworkPolicies, affinity, taints and tolerations.
* Simulated pod failures, unhealthy containers, failed deployments, resource pressure and scheduling scenarios to validate Kubernetes recovery mechanisms.
* Implemented rolling update and rollback strategies and documented failure scenarios, recovery procedures, troubleshooting steps and evidence in GitHub.

---

# 👩‍💻 Author

**Chamundeswari JangamReddy**

GitHub: `JangamReddy05`

---

# ⭐ Project Goal

> **Build it. Break it. Recover it. Prove it.**

KubeRescue demonstrates that Kubernetes is not only a platform for deploying applications, but also provides mechanisms for **self-healing, availability, scaling, scheduling, storage, security, and controlled application recovery**.
