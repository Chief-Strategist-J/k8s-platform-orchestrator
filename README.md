# LLMObs Kubernetes Platform Orchestrator

[![Go Version](https://img.shields.io/badge/go-1.21%2B-blue.svg)](https://golang.org)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

Open-standard Go orchestration engine and ArgoCD GitOps controller for the **LLM Observability & Infrastructure Platform** on Kubernetes.

---

## Architecture Overview

Built following **Hexagonal Architecture (Ports & Adapters)**, **Zero-Inline-Comment Doctrine**, and strict **Single Responsibility Principle (SRP)**:

```
packages/k8s-platform-orchestrator/
├── config/
│   ├── default.yaml
│   └── k8s/
│       ├── apps/            # ArgoCD Application & ApplicationSet CRD manifests
│       └── base/            # Kubernetes Deployments, StatefulSets, Services, Ingress
├── contracts/               # OpenAPI 3.1.0 specifications
├── src/
│   ├── api/rest/            # REST API daemon handlers
│   ├── cmd/                 # Cobra CLI commands (up, down, sync, health, scale, etc.)
│   ├── features/            # Isolated business domain modules
│   │   ├── argocd/          # ArgoCD Application & GitOps sync lifecycle
│   │   ├── backup/          # Velero & VolumeSnapshot DR
│   │   ├── certs/           # Cert-manager & TLS secret manager
│   │   ├── config/          # ResourceQuota & LimitRange tuning
│   │   ├── grafana/         # K8s-native Grafana datasources, dashboards, and alerts
│   │   ├── health/          # Concurrent diagnostic health probes across K8s workloads
│   │   ├── k8s/             # Namespace, pod, service, and workload managers
│   │   ├── ports/           # Port-forward and service ingress tunnels
│   │   ├── scale/           # HPA and StatefulSet/Deployment replica scaling
│   │   ├── services/        # External services catalog & K8s secret syncing
│   │   ├── setup/           # Cluster bootstrapping pipeline
│   │   └── stack/           # Profile resolution and ArgoCD stack orchestration
│   ├── infra/               # Infrastructure adapters (Kubernetes client, ArgoCD API)
│   └── shared/              # Hexagonal port interfaces, path resolver, and API envelopes
└── tests/                   # Unit and integration test suites
```
