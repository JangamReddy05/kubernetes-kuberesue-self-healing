# 🚀 KubeRescue — Kubernetes Autonomous Self-Healing & Fault Recovery Platform

KubeRescue is a Kubernetes-based **self-healing and fault-recovery platform** designed to demonstrate how Kubernetes can automatically detect failures, maintain application availability, recover workloads, preserve persistent data, and safely recover from failed deployments.

The project intentionally introduces different failure scenarios and validates Kubernetes-native recovery mechanisms such as **Deployments, ReplicaSets, Liveness Probes, Readiness Probes, HPA, PDB, PV/PVC, ConfigMaps, Secrets, NetworkPolicies, Rolling Updates, Rollbacks, Node Affinity, Taints, and Tolerations**.

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

# 🏗️ Architecture

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

# 📁 Project Structure

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
