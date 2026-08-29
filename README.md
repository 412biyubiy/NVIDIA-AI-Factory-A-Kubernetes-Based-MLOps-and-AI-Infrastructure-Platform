# NVIDIA-AI-Factory-A-Kubernetes-Based-MLOps-and-AI-Infrastructure-Platform
> A local GPU-enabled AI platform that integrates Kubernetes, GPU workload management, model training, model serving, MLOps, observability, GitOps, multi-tenancy, automated retraining, disaster recovery, and FinOps.

### Infrastructure

![Linux](https://img.shields.io/badge/Linux-Ubuntu-E95420)
![WSL2](https://img.shields.io/badge/WSL2-enabled-4D4D4D)
![NVIDIA](https://img.shields.io/badge/NVIDIA-GPU-76B900)
![CUDA](https://img.shields.io/badge/CUDA-12.x-76B900)
![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED)
![NVIDIA Container Toolkit](https://img.shields.io/badge/NVIDIA_Container_Toolkit-GPU-76B900)

### Kubernetes Platform

![Kubernetes](https://img.shields.io/badge/Kubernetes-Minikube-326CE5)
![Helm](https://img.shields.io/badge/Helm-Package_Manager-0F1689)
![Istio](https://img.shields.io/badge/Istio-Service_Mesh-466BB0)
![Kueue](https://img.shields.io/badge/Kueue-Workload_Scheduling-326CE5)
![NVIDIA Device Plugin](https://img.shields.io/badge/NVIDIA_Device_Plugin-GPU_Scheduling-76B900)

### MLOps

![Python](https://img.shields.io/badge/Python-3.11-blue)
![DVC](https://img.shields.io/badge/DVC-Data_Versioning-13ADC7)
![MLflow](https://img.shields.io/badge/MLflow-Experiment_Tracking-0194E2)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Metadata_DB-336791)
![MinIO](https://img.shields.io/badge/MinIO-Object_Storage-C72E49)
![Argo Workflows](https://img.shields.io/badge/Argo_Workflows-Workflow_Orchestration-EF7B4D)

### Model Serving

![KServe](https://img.shields.io/badge/KServe-Model_Serving-FF6F00)
![NVIDIA Triton](https://img.shields.io/badge/NVIDIA_Triton-Inference_Server-76B900)

### Observability

![Prometheus](https://img.shields.io/badge/Prometheus-Monitoring-E6522C)
![Grafana](https://img.shields.io/badge/Grafana-Observability-F46800)
![Loki](https://img.shields.io/badge/Loki-Logging-F46800)
![Grafana Alloy](https://img.shields.io/badge/Grafana_Alloy-Telemetry-F46800)
![Alertmanager](https://img.shields.io/badge/Alertmanager-Alerting-E6522C)
![DCGM Exporter](https://img.shields.io/badge/NVIDIA_DCGM-GPU_Monitoring-76B900)

### ML Operations & Automation

![Evidently](https://img.shields.io/badge/Evidently-ML_Drift_Monitoring-5B5BD6)
![Argo Events](https://img.shields.io/badge/Argo_Events-Event_Driven-EF7B4D)
![Argo CD](https://img.shields.io/badge/Argo_CD-GitOps-EF7B4D)

### Operations

![Velero](https://img.shields.io/badge/Velero-Disaster_Recovery-00A4EF)
![OpenCost](https://img.shields.io/badge/OpenCost-FinOps-326CE5)
![Git](https://img.shields.io/badge/Git-Version_Control-F05032)

---

## Overview

**NVIDIA AI Factory** is a Kubernetes-based AI infrastructure and MLOps platform designed to run an end-to-end machine learning lifecycle in a local GPU-enabled environment.

Instead of relying on managed Kubernetes or a cloud provider, the platform is designed to run locally using **Windows + WSL2/Ubuntu + NVIDIA GPU + Docker + Minikube**.

The platform connects infrastructure and machine learning operations into a single workflow:

```text
Infrastructure
      ↓
Kubernetes
      ↓
GPU Workload
      ↓
Training
      ↓
Model Registry
      ↓
Model Serving
      ↓
Inference
      ↓
Observability
      ↓
Drift Detection
      ↓
Automated Retraining
      ↓
Model Registry
```

The project focuses not only on running an ML model, but on building the **platform infrastructure around the complete ML lifecycle**.

The architecture integrates:

* GPU-enabled container infrastructure
* Kubernetes
* GPU scheduling
* MLOps
* Model serving
* Workload scheduling
* Observability
* Multi-tenancy
* GitOps
* Data drift monitoring
* Automated retraining
* Disaster recovery
* FinOps / cost visibility

---

## Architecture

The platform is organized into multiple architectural layers, from the underlying compute environment up to automated ML operations.

```text
┌────────────────────────────────────────────────────────────────────────┐
|                          NVIDIA AI FACTORY                             │ 
|────────────────────────────────────────────────────────────────────────│
| LAYER 0  | HOST / COMPUTE                                              |
| LAYER 1  | KUBERNETES CONTROL PLANE / PLATFORM                         |                          
| LAYER 2A | MULTI-TENANCY / RBAC / RESOURCE GOVERNANCE / GPU SCHEDULING │
| LAYER 3  | GITOPS CONTROL PLANE                                        │
| LAYER 4  | DATA / CODE / MODEL VERSIONING                              │
| LAYER 5  | TRAINING / MLOPS PIPELINE                                   │
| LAYER 6  | MODEL SERVING                                               │
| LAYER 7  | MODEL LIFECYCLE                                             │
| LAYER 8  | INFERENCE OBSERVABILITY / DRIFT                             │
| LAYER 9  | AUTOMATED RETRAINING EVENT FLOW                             │
| LAYER 10 | OBSERVABILITY PLATFORM                                      │
| LAYER 11 | ALERTING                                                    │
| LAYER 12 | DISASTER RECOVERY                                           │
| LAYER 13 | FINOPS / COST VISIBILITY                                    │
| LAYER 14 | CORE STORAGE ARCHITECTURE                                   │
└────────────────────────────────────────────────────────────────────────┘

```

### End-to-End Flow

```text
Data Scientist / ML Engineer
            │
            ▼
       Git + DVC
            │
            ▼
          MinIO
            │
            ▼
     Argo Workflows
            │
            ▼
          Kueue
            │
            ▼
     Training Workload
       │      │      │
       ▼      ▼      ▼
     DVC   MLflow   MinIO
              │
              ▼
        Model Registry
              │
              ▼
          KServe
              │
              ▼
           Triton
              │
              ▼
         Istio Gateway
              │
              ▼
        Inference Client
              │
              ▼
       Drift Detection
              │
              ▼
         Evidently AI
              │
              ▼
        Pushgateway
              │
              ▼
         Prometheus
              │
              ▼
        Alertmanager
              │
              ▼
        Argo Events
              │
              ▼
       Argo Workflows
              │
              ▼
        Retraining
              │
              ▼
           MLflow
```

The platform also has a separate operational plane:

```text
Kubernetes
    │
    ├── Prometheus ───────► Grafana
    │
    ├── DCGM Exporter ────► Prometheus
    │
    ├── Alloy ────────────► Loki ─────► Grafana
    │
    ├── OpenCost ─────────► Prometheus ─────► Grafana
    │
    └── Velero ───────────► MinIO
```

---

# Technology Stack

| Layer               | Technology               | Responsibility                            |
| ------------------- | ------------------------ | ----------------------------------------- |
| Host                | Windows                  | Host operating system                     |
| Linux               | WSL2 / Ubuntu            | Linux execution environment               |
| GPU                 | NVIDIA GPU               | AI compute                                |
| Container Runtime   | Docker Engine            | Container execution                       |
| GPU Runtime         | NVIDIA Container Toolkit | GPU access inside containers              |
| AI Container        | NVIDIA NGC PyTorch       | GPU-enabled ML environment                |
| Kubernetes          | Minikube                 | Local Kubernetes cluster                  |
| CLI                 | kubectl                  | Kubernetes management                     |
| Package Manager     | Helm                     | Kubernetes package management             |
| Service Mesh        | Istio                    | Traffic management and service networking |
| GPU Integration     | NVIDIA Device Plugin     | Exposes `nvidia.com/gpu`                  |
| Scheduling          | Kueue                    | Workload queueing and admission           |
| Workflow            | Argo Workflows           | Training/retraining orchestration         |
| GitOps              | Argo CD                  | Declarative deployment and reconciliation |
| Events              | Argo Events              | Event-driven automation                   |
| Dataset Versioning  | DVC                      | Dataset versioning and reproducibility    |
| Experiment Tracking | MLflow                   | Experiment tracking                       |
| Model Registry      | MLflow                   | Model lifecycle and metadata              |
| Metadata DB         | PostgreSQL               | MLflow metadata storage                   |
| Object Storage      | MinIO                    | Dataset, model and artifact storage       |
| Model Serving       | KServe                   | Model-serving abstraction                 |
| Inference Runtime   | Triton Inference Server  | Model inference runtime                   |
| Drift Monitoring    | Evidently AI             | Data/feature drift analysis               |
| Metrics             | Prometheus               | Metrics storage and alert evaluation      |
| GPU Metrics         | NVIDIA DCGM Exporter     | GPU telemetry                             |
| Logs                | Grafana Alloy            | Kubernetes log collection                 |
| Log Storage         | Loki                     | Log storage and querying                  |
| Visualization       | Grafana                  | Metrics/log dashboards                    |
| Alerting            | Alertmanager             | Alert routing                             |
| Backup              | Velero                   | Kubernetes backup and restore             |
| FinOps              | OpenCost                 | Resource cost visibility                  |

The technology stack and component responsibilities follow the project's architecture definition.

---

# Project Phases

## Phase 1 — AI Infrastructure Foundation

Build the underlying GPU-capable container environment.

```text
WSL / Ubuntu
     ↓
NVIDIA GPU
     ↓
Docker
     ↓
NVIDIA Container Toolkit
     ↓
NVIDIA NGC
     ↓
PyTorch Container
     ↓
PyTorch GPU Validation
```

The final validation confirms that PyTorch running inside the NVIDIA container can access the GPU.

---

## Phase 2 — Kubernetes AI Platform

Deploy the Kubernetes layer on top of the container infrastructure.

Key components:

* Minikube
* kubectl
* Helm
* Metrics Server
* NVIDIA Device Plugin
* Istio

The NVIDIA Device Plugin exposes the GPU to Kubernetes as:

```text
nvidia.com/gpu
```

For the WSL2 environment, the project uses the NVIDIA Device Plugin rather than NVIDIA GPU Operator because the NVIDIA driver is managed by Windows/WSL2.

---

## Phase 3 — AI Inference Platform

Validate model serving using **Triton Inference Server**.

This phase intentionally starts with CPU-based inference validation.

The objective is to validate:

* Kubernetes deployment
* Service networking
* Triton health checks
* HTTP inference endpoint
* gRPC endpoint
* Prometheus metrics
* Basic inference serving

Triton exposes:

```text
8000 → HTTP inference
8001 → gRPC inference
8002 → Metrics
```

---

## Phase 4 — AI Training & MLOps Pipeline

Build a reproducible ML training pipeline.

```text
Git
 │
 ├── train.py
 ├── dvc.yaml
 └── params.yaml
 │
 ▼
DVC
 │
 ▼
MinIO
 │
 ▼
Argo Workflows
 │
 ▼
Training Pod
 │
 ├── DVC → Dataset
 │
 ├── MLflow → Experiment Metadata
 │
 └── MinIO → Model Artifacts
 │
 ▼
PostgreSQL
```

The separation of responsibilities is intentional:

```text
Git
 └── Source code + pipeline configuration

DVC
 └── Dataset versioning

MinIO
 ├── Dataset objects
 ├── Model artifacts
 └── ML artifacts

MLflow
 └── Experiment tracking + model registry

PostgreSQL
 └── MLflow metadata
```

The training pipeline uses the California Housing dataset as the example workload, with DVC defining dependencies and outputs for reproducible training.

---

## Phase 5 — AI Workload Scheduling

Introduce **Kueue** for workload queueing and resource admission.

The scheduling architecture is:

```text
Training Workload
       ↓
   LocalQueue
       ↓
  ClusterQueue
       ↓
Admission Control
       ↓
 ┌─────┴─────┐
 ▼           ▼
ADMITTED   SUSPENDED
 │           │
 ▼           │
GPU Job ◄────┘
```

Kueue manages:

* Queueing
* Admission control
* Priority
* CPU quota
* Memory quota
* GPU quota
* Workload suspension

Argo Workflows is integrated with Kueue using:

```yaml
kueue.x-k8s.io/queue-name: mlops-queue
```

---

## Phase 6 — AI Observability Platform

Build centralized observability for:

* Kubernetes resources
* Application metrics
* GPU telemetry
* Logs
* Model metrics

### Metrics

```text
Kubernetes
    ↓
Prometheus
    ↓
Grafana
```

### GPU Metrics

```text
NVIDIA GPU
    ↓
NVML / DCGM
    ↓
DCGM Exporter
    ↓
Prometheus
    ↓
Grafana
```

Tracked GPU information includes:

* GPU utilization
* VRAM usage
* Temperature
* Power
* DCGM metrics

### Logs

```text
Kubernetes Pods
      ↓
Grafana Alloy
      ↓
Loki
      ↓
Grafana
```

---

## Phase 7 — Multi-Tenant AI Platform

Introduce namespace isolation and role-based access control.

The platform defines multiple personas:

```text
┌──────────────────────┐
│ Kubernetes Cluster   │
└──────────┬───────────┘
           │
     ┌─────┼─────┬──────────┐
     ▼     ▼     ▼          ▼
  team-ds team-mle team-pe team-intern
```

### Tenant Model

| Tenant        | Persona           | Access Model               |
| ------------- | ----------------- | -------------------------- |
| `team-ds`     | Data Scientist    | Namespace-scoped           |
| `team-mle`    | ML Engineer       | Namespace-scoped           |
| `team-pe`     | Platform Engineer | Cluster-wide               |
| `team-intern` | Intern            | Restricted / read-oriented |

RBAC is validated using:

```bash
kubectl auth can-i
```

This validates not only that RBAC resources exist, but that each persona actually receives the intended permissions.

Resource governance is separated between Kubernetes and Kueue:

```text
ResourceQuota
├── CPU
├── Memory
└── Pod Count

Kueue
└── GPU
```

This prevents multiple mechanisms from simultaneously attempting to control GPU capacity.

---

# Phase 8 — GitOps & Automated MLOps Operations

Phase 8 connects the platform components into an operational ML lifecycle.

## GitOps

```text
Git Repository
      ↓
    Argo CD
      ↓
Kubernetes API
      ↓
Running Resources
```

Argo CD continuously reconciles the desired state stored in Git with the actual state of Kubernetes.

If a resource is manually modified:

```text
Git Desired State
        ↓
      Argo CD
        ↓
Kubernetes Actual State
        ↓
    Drift Detected
        ↓
     Self-Healing
        ↓
Desired State Restored
```

The project validates GitOps by manually changing a Kubernetes resource and verifying that Argo CD restores the Git-defined state.

---

# Model Serving

The production-oriented model serving architecture uses:

```text
Client
  │
  ▼
Istio Ingress Gateway
  │
  ▼
Istio VirtualService
  │
  ▼
KServe
  │
  ▼
Triton
  │
  ▼
MinIO
  │
  ▼
Model Repository
```

Example Triton model repository:

```text
housing-model/
└── 1/
    └── model.onnx
```

KServe provides the serving abstraction and lifecycle management, while Triton acts as the inference runtime.

---

# Model Lifecycle

```text
Training
   ↓
MLflow
   ↓
Model Version
   ↓
MinIO
   ↓
KServe
   ↓
Triton
   ↓
Inference
```

MLflow manages:

* Experiments
* Runs
* Parameters
* Metrics
* Model versions
* Registry metadata

MinIO stores:

* Model artifacts
* Dataset objects
* ML artifacts
* Backup objects

PostgreSQL stores MLflow metadata.

---

# Drift Detection & Automated Retraining

The platform implements an event-driven automated retraining loop.

```text
Inference Data
      ↓
Drift Checker
      ↓
Evidently AI
      ↓
Pushgateway
      ↓
Prometheus
      ↓
Alertmanager
      ↓
Argo Events
      ↓
Argo Workflows
      ↓
Retraining
      ↓
MLflow
```

The drift signal used by the architecture is:

```text
model_data_drift_share
```

When the configured Prometheus alert threshold is exceeded, Alertmanager sends a webhook to Argo Events, which triggers the training workflow.

---

# Important Limitation

> **This project currently implements an automated retraining loop, not a fully autonomous closed-loop MLOps deployment system.**

The current flow ends at:

```text
Drift
  ↓
Alert
  ↓
Argo Events
  ↓
Argo Workflows
  ↓
Retraining
  ↓
MLflow
```

A complete autonomous model deployment lifecycle would require:

```text
Retraining
    ↓
Model Validation
    ↓
Champion vs Challenger
    ↓
Model Promotion
    ↓
Production Deployment
    ↓
Canary / Progressive Rollout
    ↓
Production Monitoring
    ↓
Rollback
```

These steps are currently outside the implemented automated loop.

This distinction is intentional: a newly retrained model should **not automatically replace the production model without validation**.

---

# Disaster Recovery

The platform uses **Velero + MinIO** for Kubernetes backup and restore.

```text
Kubernetes Cluster
        ↓
      Velero
        ↓
      MinIO
        ↓
  Backup Objects
```

Restore flow:

```text
Backup
  ↓
MinIO
  ↓
Simulated Disaster
  ↓
Namespace Deleted
  ↓
Velero Restore
  ↓
Namespace Recreated
  ↓
Pods Recreated
  ↓
Application Validation
```

---

# FinOps / Cost Visibility

OpenCost is used to provide resource cost visibility.

```text
Kubernetes
    │
    ├── CPU
    ├── Memory
    ├── GPU
    ├── Storage
    └── Network
          │
          ▼
       OpenCost
          │
          ▼
      Prometheus
          │
          ▼
        Grafana
```

Cost visibility can be broken down by namespace, including:

```text
team-ds
team-mle
team-pe
team-intern
mlops
kube-system
```

The pricing model used in this project represents **simulated local-lab costs**, not actual cloud-provider pricing.

---

# Storage Architecture

MinIO acts as the central object storage layer.

```text
                    ┌──────────────┐
                    │    MinIO     │
                    └──────┬───────┘
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
     DVC Dataset      MLflow Artifacts   Velero Backups
          │                │                │
     datasets/          models/       velero-backup/
```

MLflow additionally uses PostgreSQL for structured metadata:

```text
MLflow
   │
   ├── Run Metadata
   ├── Parameters
   ├── Metrics
   ├── Tags
   └── Registry Metadata
          │
          ▼
      PostgreSQL
```

---

# Communication Architecture

| Connection                      | Function                        |
| ------------------------------- | ------------------------------- |
| kubectl → Kubernetes API        | Manage Kubernetes resources     |
| Helm → Kubernetes API           | Install and manage packages     |
| Argo CD → Git                   | Read desired state              |
| Argo CD → Kubernetes API        | Reconcile desired state         |
| DVC → MinIO                     | Dataset upload/download         |
| Argo Workflows → Kubernetes API | Execute workflows               |
| Training Pod → MinIO            | Dataset/model artifact transfer |
| Training Pod → MLflow           | Metrics and run metadata        |
| MLflow → PostgreSQL             | Metadata storage                |
| MLflow → MinIO                  | Artifact storage                |
| KServe → Kubernetes API         | InferenceService lifecycle      |
| KServe → MinIO                  | Model retrieval                 |
| KServe → Triton                 | Model inference                 |
| Client → Istio Gateway          | Inference requests              |
| Istio → KServe/Triton           | Traffic routing                 |
| Triton → Client                 | Prediction response             |
| Evidently → Pushgateway         | Drift metrics                   |
| Prometheus → Pushgateway        | Metric scraping                 |
| Prometheus → DCGM Exporter      | GPU telemetry                   |
| Grafana → Prometheus            | Metrics queries                 |
| Grafana → Loki                  | Log queries                     |
| Alertmanager → Argo Events      | Automation webhook              |
| Argo Events → Argo Workflows    | Retraining trigger              |
| Velero → MinIO                  | Backup storage                  |
| Kueue → Workload                | Admission and suspension        |

---

# Project Structure

The GitOps repository is organized around the platform phases.

```text
ai-factory/
│
├── phase4/
│   ├── minio-values.yaml
│   ├── mlflow.yaml
│   ├── mlflow-service.yaml
│   └── argo-training-workflow.yaml
│
├── phase5/
│   └── kueue/
│       ├── cluster-queue.yaml
│       ├── local-queue.yaml
│       └── ...
│
├── phase6/
│   └── monitoring/
│       ├── prometheus/
│       ├── grafana/
│       ├── loki/
│       └── dcgm/
│
├── phase7/
│   └── multi-tenant/
│       ├── namespaces/
│       ├── rbac/
│       ├── resourcequota/
│       └── limitrange/
│
└── phase8/
    ├── argocd/
    ├── kserve/
    ├── istio/
    ├── drift/
    ├── retraining/
    ├── velero/
    └── opencost/
```

> The exact repository structure may evolve as the implementation is consolidated into the GitOps repository.

---

# Getting Started

## Prerequisites

The platform is designed around:

* Windows host
* WSL2
* Ubuntu
* NVIDIA GPU
* NVIDIA GPU driver
* Docker Engine
* NVIDIA Container Toolkit
* Minikube
* kubectl
* Helm

Verify the GPU from WSL:

```bash
nvidia-smi
```

Verify Docker:

```bash
docker --version
```

Verify Kubernetes:

```bash
kubectl version --client
minikube version
```

Verify Helm:

```bash
helm version
```

---

# GPU Container Validation

Pull the NVIDIA PyTorch container:

```bash
docker pull nvcr.io/nvidia/pytorch:25.06-py3
```

Run with GPU access:

```bash
docker run --rm -it \
  --gpus all \
  nvcr.io/nvidia/pytorch:25.06-py3
```

Then:

```python
import torch

torch.cuda.is_available()
torch.cuda.get_device_name(0)
```

This validates the chain:

```text
NVIDIA GPU
    ↓
WSL2
    ↓
Docker
    ↓
NVIDIA Container Toolkit
    ↓
NVIDIA Container
    ↓
PyTorch
```

---

# Kubernetes GPU Validation

Install the NVIDIA Device Plugin:

```bash
helm repo add nvidia https://helm.ngc.nvidia.com/nvidia
helm repo update

helm install nvdp nvidia/nvidia-device-plugin
```

Check GPU availability:

```bash
kubectl describe node minikube
```

The node should expose:

```text
nvidia.com/gpu
```

---

# Triton Validation

Check Triton:

```bash
kubectl get pods -n ai
kubectl get svc -n ai
```

Port-forward the inference API:

```bash
kubectl port-forward svc/triton -n ai 8000:8000
```

Health check:

```bash
curl localhost:8000/v2/health/live
curl localhost:8000/v2/health/ready
```

Metrics:

```bash
kubectl port-forward svc/triton -n ai 8002:8002
```

Then:

```bash
curl localhost:8002/metrics
```

---

# GitOps

Argo CD is used to continuously reconcile Kubernetes resources from Git.

Basic validation:

```bash
kubectl get pods -n argocd

argocd app list

argocd app get ai-factory-phase4
```

Manual synchronization:

```bash
argocd app sync ai-factory-phase4
```

GitOps self-healing can be tested by manually changing a Kubernetes deployment:

```bash
kubectl edit deployment mlflow -n mlops
```

Argo CD should restore the resource to the state defined in Git.

---

# End-to-End Validation

The platform includes an end-to-end validation workload to verify that Kubernetes workloads can run and their resource consumption can be observed by OpenCost.

Example workload:

```text
team-ds
   ↓
E2E Workload
   ↓
CPU / Memory Consumption
   ↓
OpenCost
   ↓
Namespace Cost Allocation
```

Example validation:

```bash
kubectl get pod e2e-test-workload -n team-ds
```

OpenCost:

```bash
kubectl port-forward \
  -n opencost \
  svc/opencost \
  9999:9003
```

Query namespace allocation:

```bash
curl \
"http://localhost:9999/allocation/compute?window=10m&aggregate=namespace&filter=namespace:\"team-ds\""
```

---

# Design Principles

## 1. Layered Architecture

Each component belongs to a specific architectural layer and has a defined responsibility.

```text
Infrastructure
      ↓
Kubernetes
      ↓
Platform Services
      ↓
MLOps
      ↓
Model Serving
      ↓
Observability
      ↓
Automation
```

## 2. Kubernetes as the Execution Platform

Kubernetes is the primary execution environment for:

* AI workloads
* Training
* Model serving
* Monitoring
* Automation

## 3. Declarative Infrastructure

Platform configuration is defined declaratively and managed through GitOps.

```text
Git
 ↓
Desired State
 ↓
Argo CD
 ↓
Kubernetes
```

## 4. Separation of Responsibilities

Each tool has a distinct responsibility.

```text
Kueue
→ Workload admission / queueing

MLflow
→ Experiment tracking / model registry

MinIO
→ Object storage

PostgreSQL
→ Structured MLflow metadata

KServe
→ Model-serving abstraction

Triton
→ Inference runtime

Argo Workflows
→ Workflow execution

Argo CD
→ Infrastructure reconciliation
```

## 5. Observable by Design

Workloads are designed to expose operational signals:

```text
Metrics
Logs
GPU Telemetry
Model Metrics
Drift Metrics
```

## 6. Automated ML Lifecycle

Training, registration, monitoring, drift detection, and retraining are connected into an automated pipeline.

However:

> Automated retraining does not automatically mean autonomous model deployment.

Model validation and promotion remain a separate concern.

---

# Current State

| Capability                           | Status              |
| ------------------------------------ | ------------------- |
| GPU-enabled container infrastructure | Implemented         |
| NVIDIA GPU → Docker                  | Implemented         |
| PyTorch GPU validation               | Implemented         |
| Minikube Kubernetes platform         | Implemented         |
| Kubernetes GPU integration           | Implemented         |
| Istio                                | Implemented         |
| Triton inference validation          | Implemented         |
| DVC                                  | Implemented         |
| MinIO                                | Implemented         |
| MLflow                               | Implemented         |
| PostgreSQL                           | Implemented         |
| Argo Workflows                       | Implemented         |
| Kueue                                | Implemented         |
| Prometheus                           | Implemented         |
| Grafana                              | Implemented         |
| GPU monitoring                       | Implemented         |
| Loki + Alloy                         | Implemented         |
| Alertmanager                         | Implemented         |
| Multi-tenancy / RBAC                 | Implemented         |
| Argo CD GitOps                       | Implemented         |
| KServe                               | Implemented         |
| Evidently drift monitoring           | Implemented         |
| Automated retraining trigger         | Implemented         |
| Velero backup / restore              | Implemented         |
| OpenCost                             | Implemented         |
| Champion vs Challenger               | Not yet automated   |
| Automated model promotion            | Not yet automated   |
| Automated production rollout         | Not yet automated   |
| Automated rollback                   | Not yet automated   |
| Fully autonomous closed-loop MLOps   | Not yet implemented |

---

# What This Project Demonstrates

This project demonstrates the design and integration of an AI platform across several infrastructure domains:

### Cloud / Platform Engineering

* Kubernetes
* Containerization
* Resource governance
* Workload scheduling
* GitOps
* Infrastructure automation

### MLOps

* Dataset versioning
* Reproducible training
* Experiment tracking
* Model registry
* Model serving
* Drift detection
* Automated retraining

### GPU Infrastructure

* NVIDIA GPU
* CUDA
* NVIDIA Container Toolkit
* NVIDIA Device Plugin
* GPU scheduling
* GPU telemetry

### Observability

* Prometheus
* Grafana
* Loki
* Grafana Alloy
* NVIDIA DCGM Exporter
* Alertmanager

### Platform Security / Governance

* Kubernetes RBAC
* Namespace isolation
* ResourceQuota
* LimitRange
* Tenant separation

### Operations

* GitOps
* Disaster recovery
* Cost visibility
* Automated event processing

---

# Platform Lifecycle

The overall lifecycle can be summarized as:

```text
Infrastructure
      ↓
Kubernetes
      ↓
GPU Availability
      ↓
Workload Scheduling
      ↓
Training
      ↓
Experiment Tracking
      ↓
Model Registry
      ↓
Model Serving
      ↓
Inference Traffic
      ↓
Observability
      ↓
Drift Detection
      ↓
Alert
      ↓
Automated Retraining
      ↓
New Model
      ↓
Model Registry
```

Meanwhile, the platform deployment lifecycle is:

```text
Git Repository
      ↓
Argo CD
      ↓
Desired State
      ↓
Kubernetes
      ↓
Running Platform
```

These two lifecycle loops meet at Kubernetes, which acts as the primary execution platform.

---

# Future Improvements

The most important next step is completing the model deployment control loop:

```text
Automated Retraining
        ↓
Model Validation
        ↓
Champion vs Challenger
        ↓
Quality Gate
        ↓
Model Promotion
        ↓
KServe Model Update
        ↓
Canary Deployment
        ↓
Production Monitoring
        ↓
Automatic Rollback
```

This would transform the current **automated retraining loop** into a more complete **closed-loop MLOps system**.

---

# Project Philosophy

The goal of NVIDIA AI Factory is not to demonstrate the maximum number of tools.

The goal is to demonstrate how different infrastructure and MLOps components can be connected while maintaining clear separation of responsibilities.

```text
Infrastructure
      +
Kubernetes
      +
GPU
      +
MLOps
      +
Model Serving
      +
Observability
      +
Security / Governance
      +
GitOps
      +
Automation
      =
AI Platform
```

---

# Author

**Abiyu Salam**

Computer Science — Artificial Intelligence

---

## Disclaimer

This project is a **local AI infrastructure and MLOps laboratory environment** designed for learning, experimentation, architecture validation, and portfolio development.

It is intentionally implemented on a constrained local environment and should not be interpreted as a production-scale NVIDIA AI Factory deployment.

The architecture is designed to demonstrate the concepts and integration patterns behind a modern AI platform while remaining feasible to run locally.
