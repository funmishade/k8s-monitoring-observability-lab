# k8s-monitoring-observability-lab
Hands-on Kubernetes observability lab using Prometheus, Grafana, and Alertmanager with application-level metrics and SRE-style alerting.

# Kubernetes Monitoring & Alerting with Prometheus and Grafana

## 📌 Overview
This project implements a production-grade monitoring and alerting system for Kubernetes infrastructure and applications using **Prometheus**, **Grafana**, and **Alertmanager**.

The setup provides real-time visibility into:
- Cluster and node health
- Pod and application resource usage
- Proactive alerting via email notifications

The project is deployed on a **KIND Kubernetes cluster** and follows cloud-native best practices.

---

## 🏗️ Architecture

Metrics are collected from Kubernetes nodes and applications using exporters and scraped by Prometheus. Grafana visualizes these metrics, while Alertmanager handles alert notifications.

---

## 🧰 Tech Stack
- Kubernetes (KIND)
- Helm
- Prometheus
- Grafana
- Alertmanager
- Node Exporter
- kube-state-metrics
- Nginx (sample application)

---

## 🚀 Features
- Cluster-wide monitoring (CPU, memory, disk, network)
- Application-level monitoring (pod metrics)
- Custom Prometheus alert rules
- Email alerting using Gmail SMTP
- Grafana dashboards for infrastructure and apps
- Kubernetes-native service discovery

---

## 🔧 Setup Summary

1. Create monitoring namespace
2. Install kube-prometheus-stack via Helm
3. Deploy sample application (nginx)
4. Configure Prometheus alert rules
5. Configure Alertmanager email notifications
6. Visualize metrics in Grafana

---

## 🔔 Alerting
Alerts are defined using PrometheusRule CRDs and routed through Alertmanager. Notifications are sent via Gmail when alert thresholds are exceeded.

---

## 📊 Dashboards
- Node resource usage
- Pod CPU & memory usage
- Application load behavior

---

## 🧠 Key Learnings
- Kubernetes observability
- PromQL querying
- Helm-based configuration management
- Alert fatigue prevention
- Production monitoring patterns

---

## 🔜 Future Improvements
- Add application-level metrics via ServiceMonitor
- Integrate Grafana Loki for logs
- Add SLO-based alerting
- Monitor multiple applications

---

## 📄 License
MIT

+----------------------+
|   Kubernetes Nodes   |
|  (KIND Cluster)      |
+----------+-----------+
           |
           | Metrics
           v
+----------------------+
| Exporters            |
| - node-exporter      |
| - kube-state-metrics |
| - app metrics        |
+----------+-----------+
           |
           | Scrape
           v
+----------------------+
| Prometheus           |
| - TSDB               |
| - PromQL             |
+----------+-----------+
           |
   +-------+-------+
   |               |
   v               v
+--------+     +------------+
| Grafana|     | Alertmanager|
| Dashbd |     | Notifications|
+--------+     +------------+
                    |
                    v
              Email (Gmail)



# Kubernetes Monitoring & Alerting Lab (Prometheus + Grafana)

## 📌 Project Overview

This project demonstrates how to build a **production-style monitoring and alerting system** for Kubernetes workloads using **Prometheus, Grafana, and Alertmanager** on a **KIND (Kubernetes in Docker)** cluster.  
It includes application metrics, ServiceMonitors, alerting, and email notifications.

The goal is to gain hands-on experience with **observability**, **SRE-style alerting**, and **DevOps troubleshooting**, producing a portfolio-ready project for interviews.

---

## 🎯 Objectives

- Deploy Prometheus, Grafana, and Alertmanager on Kubernetes
- Monitor cluster, node, and application-level metrics
- Expose application metrics using ServiceMonitor
- Configure alerting rules and send alerts to Gmail
- Visualize metrics in Grafana dashboards
- Practice troubleshooting common Kubernetes monitoring issues

---

## 🛠️ Tech Stack

- Kubernetes (KIND)
- Prometheus Operator (kube-prometheus-stack)
- Prometheus
- Grafana
- Alertmanager
- Nginx (demo application)
- PromQL
- YAML / Kubernetes Manifests

---

## 🧱 Architecture Overview

![Architecture Diagram](docs/architecture-diagram.png)

[ Application Pods ]
|
v
[ Service + ServiceMonitor ]
|
v
[ Prometheus ] -----> [ Grafana Dashboards ]
|
v
[ Alertmanager ] -----> [ Gmail Alerts ]

yaml
Copy code

---

## 📂 Repository Structure

k8s-monitoring-lab/
├── README.md
├── k8s/
│ ├── demo-nginx.yaml
│ ├── servicemonitor-demo-nginx.yaml
│ ├── prometheus-alert-rules.yaml
│ └── alertmanager-gmail-secret.yaml
├── docs/
│ ├── architecture-diagram.png
│ ├── screenshots/
│ └── changelog.md

yaml
Copy code

---

## 🚀 Lab Phases

### Phase 1: Cluster Setup
- Create KIND cluster
- Verify kubectl connectivity

### Phase 2: Monitoring Stack Installation
- Install kube-prometheus-stack using Helm
- Verify Prometheus, Grafana, and Alertmanager pods

### Phase 3: Application Deployment
- Deploy demo Nginx application
- Expose metrics endpoint

### Phase 4: Metrics & Dashboards
- Validate Prometheus scrape targets
- Create Grafana dashboards
- Test PromQL queries

### Phase 5: Alerting
- Configure Prometheus alert rules
- Configure Alertmanager email notifications
- Test alerts via traffic simulation

---

## 🔔 Alerting Setup (Email)

Alerts are configured using **PrometheusRule** objects and routed via **Alertmanager** to Gmail SMTP.

Example alerts include:
- Pod down
- High request rate
- Service unavailable

---

## 🧪 Testing & Validation

- Port-forward Prometheus, Grafana, and Alertmanager
- Generate traffic to trigger alerts
- Confirm alert delivery via email

---

## ⚠️ Errors Encountered & Fixes

| Issue                         | Cause                         | Resolution                         |
| ----------------------------- | ----------------------------- | ---------------------------------- |
| Port already in use           | Existing process on localhost | Changed port-forward port          |
| Alertmanager config read-only | Operator-managed config       | Used Kubernetes Secret             |
| No alerts firing              | No active rules               | Added PrometheusRule               |
| Service not found             | Incorrect service name        | Listed services and corrected name |

---

## 📘 Key Learnings

- Prometheus Operator manages configs declaratively
- Alertmanager configs must be injected via Secrets
- ServiceMonitors are namespace-sensitive
- Monitoring Kubernetes requires understanding services, labels, and selectors

---

## 🧑‍💻 Interview Talking Points

- Designed Kubernetes observability using Prometheus and Grafana
- Implemented application-level monitoring using ServiceMonitors
- Built alerting pipelines with Alertmanager and email notifications
- Troubleshot real-world Kubernetes and networking issues

---

## 📌 Next Enhancements

- Add frontend, backend, and API microservices
- Add SLO-based alerting
- Integrate Loki for logs
- Add recording rules for performance
- Deploy to cloud (EKS / GKE / AKS)

---

## 📎 References

- [Prometheus Docs](https://prometheus.io/docs/)
- [Grafana Docs](https://grafana.com/docs/)
- Kubernetes Monitoring Best Practices



Kubernetes Monitoring & Observability Lab
Project Goal

Implement a monitoring and observability system for a Kubernetes cluster using:

Prometheus → collects metrics

Grafana → visualizes metrics

Alertmanager → sends alerts

Focus: cluster health, node metrics, and pod metrics. App-level metrics are limited since the app image does not expose /metrics yet.

Prerequisites

KIND cluster running

kubectl configured

Helm installed

Existing Nginx / backend / frontend deployments

Prometheus + Grafana installed via Helm

Phase 1: Setup Namespace
kubectl create namespace apps
kubectl create namespace monitor

Phase 2: Deploy Prometheus & Grafana via Helm
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

helm install kube-stack prometheus-community/kube-prometheus-stack -n monitor


Check pods:

kubectl get pods -n monitor


Access Grafana UI:

export POD_NAME=$(kubectl get pod -n monitor -l "app.kubernetes.io/name=grafana,app.kubernetes.io/instance=kube-stack" -o name)
kubectl port-forward $POD_NAME 3000:80 -n monitor

Phase 3: Verify Prometheus Targets

Open Prometheus UI: http://localhost:9090

Go to Status → Targets

Confirm:

node-exporter → UP

kube-state-metrics → UP

Phase 4: Deploy Node & Cluster Metrics Monitoring

Node metrics are already collected via node-exporter.
Kubernetes object state metrics via kube-state-metrics.

No app-level metrics yet because /metrics is missing in the backend/frontend images.

Phase 5: Create a ServiceMonitor for backend (optional)

Only works if your app exposes /metrics. Currently, it won’t scrape anything.

Example servicemonitor.yaml:

apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: backend-api-monitor
  namespace: apps
spec:
  selector:
    matchLabels:
      app: backend-api
  endpoints:
    - port: "8081"
      path: /metrics
      interval: 15s


Apply it:

kubectl apply -f servicemonitor.yaml


Note: This will be useless until the backend image exposes /metrics.

Phase 6: Grafana Dashboards

Open Grafana: http://localhost:3000

Add Prometheus as a data source

Create dashboards for:

Node metrics → CPU, Memory, Disk, Network

Pod metrics → Ready status, Restarts, Age

Deployment metrics → Replicas, Pod count

Optional: use Grafana dashboard library → "Kubernetes cluster monitoring"

Phase 7: Alerts

Example alert rules:

groups:
- name: node-alerts
  rules:
  - alert: NodeHighCPU
    expr: node_cpu_seconds_total{mode="idle"} < 20
    for: 1m
    labels:
      severity: warning
    annotations:
      summary: "Node CPU usage is high"


Apply via PrometheusRule or directly in Prometheus

Configure Alertmanager for email/Slack notifications

Test alerts → cluster nodes going high CPU, pod down, etc.

Phase 8: What is Working / Not Working

✅ Working:

Cluster monitoring via node-exporter

Kubernetes object monitoring via kube-state-metrics

Grafana dashboards visualizing node & pod metrics

Alerts for nodes/pods

❌ Not Working / Needs Improvement:

Backend & frontend app metrics are not exposed (no /metrics)
→ Without this, ServiceMonitor cannot scrape app metrics
→ To fix: use an image with Prometheus instrumentation or instrument the app

Phase 9: Next Steps / Improvements

Replace backend image with one exposing /metrics

Add frontend metrics for user experience (latency, request success rate)

Add database metrics if running a DB (MySQL/MongoDB exporters)

Integrate Loki for log aggregation and connect to Grafana

Phase 10: Commands Reference
# View pods
kubectl get pods -n monitor
kubectl get pods -n apps

# Port-forward Grafana
kubectl port-forward svc/prometheus-stack-grafana 3000:80 -n monitor

# Port-forward Prometheus
kubectl port-forward svc/prometheus-stack-kube-prom-prometheus 9090:9090 -n monitor

# Apply ServiceMonitor / deployment
kubectl apply -f servicemonitor.yaml
kubectl apply -f deployment.yaml


✅ This README can go straight into your GitHub repo for portfolio / interview visibility.
It clearly shows what works, what is missing, and next steps, which is exactly what interviewers like.
