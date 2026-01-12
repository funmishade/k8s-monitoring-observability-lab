# Kubernetes Observability Lab (Prometheus, Grafana & Alertmanager)

## 📌 Overview

This project demonstrates **end-to-end observability in Kubernetes** using **Prometheus, Grafana, and Alertmanager**. It is designed as a **hands-on DevOps lab** to showcase monitoring, alerting, and visualization of metrics for Kubernetes clusters and applications.

This lab is ideal for:

* DevOps / Cloud Engineers
* Kubernetes beginners to intermediate learners
* Interview-ready portfolio projects

---

## 🧱 Architecture

The observability stack includes:

* **Kubernetes Cluster** (Kind / Minikube / EKS)
* **kube-prometheus-stack (Helm)**

  * Prometheus (metrics collection)
  * Grafana (dashboards & visualization)
  * Alertmanager (alerts & notifications)
* **Sample Application** (monitored app)

```
Kubernetes Cluster
│
├── Prometheus ── scrapes metrics
├── Grafana ── visualizes metrics
├── Alertmanager ── sends alerts
└── Sample App ── exposes metrics
```

---

## 🛠️ Tools & Technologies

* Kubernetes
* Helm
* Prometheus
* Grafana
* Alertmanager
* Kind / Minikube / EKS
* YAML

---

## �� Repository Structure

```
.
├── monitoring/
│   ├── 
│   ├── 
│   ├── 
│   └── 
├── k8s/
│   ├── deployment.yaml
│   ├── service.yaml
│   └── servicemonitor.yaml
├── docs/
│   └── notes.md
├── README.md
```

---

## 🚀 Prerequisites

Ensure you have the following installed:

* kubectl
* Helm (v3+)
* Docker
* Kubernetes cluster (Kind / Minikube / EKS)

Verify installation:

```bash
kubectl version --client
helm version
docker --version
```

---

## ⚙️ Step 1: Create Kubernetes Cluster (Kind Example)

```bash
kind create cluster --name observability-lab
kubectl cluster-info
```

---

## ⚙️ Step 2: Add Helm Repositories

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

---

## ⚙️ Step 3: Install kube-prometheus-stack

```bash
kubectl create namespace monitoring

helm install kube-prometheus prometheus-community/kube-prometheus-stack \
  -n monitoring \
  -f monitoring/prometheus-values.yaml
```

Verify:

```bash
kubectl get pods -n monitoring
```

---

## ⚙️ Step 4: Deploy Sample Application

```bash
kubectl apply -f app/deployment.yaml
kubectl apply -f app/service.yaml
```

Check:

```bash
kubectl get pods
kubectl get svc
```

---

## ⚙️ Step 5: Configure ServiceMonitor

This allows Prometheus to scrape metrics from the application.

```bash
kubectl apply -f app/servicemonitor.yaml
```

Verify:

```bash
kubectl get servicemonitor -n monitoring
```

---

## ⚙️ Step 6: Configure Alertmanager

Apply Alertmanager configuration:

```bash
kubectl apply -f monitoring/alertmanager-config.yaml
```

Example alerts:

* Pod down
* High CPU usage
* High memory usage

---

## ⚙️ Step 7: Access Grafana

Port-forward Grafana:

```bash
kubectl port-forward -n monitoring svc/kube-prometheus-grafana 3000:80
```

Access:

```
http://localhost:3000
```

Default credentials:

```
Username: 
Password:
```

---

## 📊 Step 8: Import Dashboards

* Import Kubernetes dashboards
* Import custom dashboards from `/dashboards`

Metrics visualized:

* Pod CPU & memory usage
* Node health
* Application request metrics

---

## 🚨 Step 9: Validate Alerts

Simulate load or pod failure:

```bash
kubectl scale deployment sample-app --replicas=0
```

Confirm alerts:

* Prometheus UI
* Alertmanager UI

---

## 🔍 Key Concepts Demonstrated

* ServiceMonitor vs Service Discovery
* Prometheus scraping
* Alert rules & burn rate alerts
* Kubernetes observability best practices
* Production-style monitoring setup

---

## 📈 What This Project Shows Recruiters

* Real-world Kubernetes monitoring
* Helm-based deployments
* YAML-driven infrastructure
* Understanding of SLI / SLO / alerts
* Hands-on DevOps experience

---

## 🧹 Cleanup

```bash
kind delete cluster --name observability-lab
```

---

## 📚 References

* [https://prometheus.io/docs/](https://prometheus.io/docs/)
* [https://grafana.com/docs/](https://grafana.com/docs/)
* [https://github.com/prometheus-community/helm-charts](https://github.com/prometheus-community/helm-charts)

---

## 👤 Author

**Funmi Adewale**
DevOps Engineer | Cloud | Kubernetes | Observability

---

⭐ If you find this useful, please star the repository!

