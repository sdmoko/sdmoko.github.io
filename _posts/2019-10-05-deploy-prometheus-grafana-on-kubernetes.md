---
layout: post
title: "Deploy Prometheus + Grafana on Kubernetes"
description: "Deploy Prometheus and Grafana for monitoring on kubernete "
comments: false
keywords: "kubernetes, k8s, kubic, prometheus, grafana"
---

## Introduction

Monitoring is a crucial aspect of any jobs for technologies like Kubernetes which is a rage right now, a robust monitoring setup can bolster your confidence to migrate production workloads from VMs to Containers.

There is a opensource monitoring solution. Prometehus and Grafana. This tools is a prefect combination for monitoring. Add alertmanager and it's a great additional to have alerting. Where prometheus server is a metric storage or time series database to store the metrics. Grafana is a visualization tools.

## Requirement

My environment uses 4 CPU cores and 8GB of RAM per node.

1 master nodes.
2 worker nodes.
100GB volume attached to worker nodes as a Persistent Volume.
You can use your kubernetes environment. I would suggest you use 8 CPUs and 8GB of RAM per node with 1 Master and 2 Worker or more.

Kubernetes 1.10+
kubectl client

## Deployment Guide

All of the YAML using in this posts is available at [https://github.com/sdmoko/k8s-prometheus-grafana](https://github.com/sdmoko/k8s-prometheus-grafana)

The steps:
1. Clone the repository on the master node

```
git clone https://github.com/sdmoko/k8s-prometheus-grafana.git
cd k8s-prometheus-grafana
```

2. We need to deploy prometheus as a metric storage (TSDB). To deploy prometheus we need to add a RBAC for prometheus.
```
kubectl apply -f prometheus/00-prometheus-rbac.yaml
```

3. Then deploy a configmap for prometheus config.
```
kubectl apply -f prometheus/01-prometheus-configmap.yaml
```

4. Then we can create a rules that will trigger the alertmanager.
```
kubectl apply -f prometheus/02-prometheus-rules.yaml
```

5. Then we can create a storage for prometheus store the data.
```
kubectl apply -f prometheus/03-prometheus-storage.yaml
```

6. Then we can create a deployment and service for prometheus.
```
kubectl apply -f prometheus/prometheus-deployment.yaml
kubectl apply -f prometheus/prometheus-service.yaml
```

7. Then we deploy kube-metrics server to expose container and pod metrics other than those exposed by cadvisor on the nodes.
```
kubectl apply -f kube-state-metrics/kube-state-metrics.yaml
```

8. Then we can deploy and provide service for grafana dashboard to visualize the monitoring data.
```
kubectl apply -f grafana/grafana-deployment.yaml
kubectl apply -f grafana/grafana-service.yaml
```

9. Then we open the grafana service from browser, and then add prometheus data source and add a dashboard. For config of the grafana data source use:
```
Name	: DS_Prometheus
Type	: Prometheus
URL		: http://prometheus-service:8080
```

![prometheus datasource](/assets/prometheus_ds.png)

10. Then we can add a dashboard. I'm using this [json](https://github.com/Thakurvaibhav/k8s/tree/master/monitoring/dashboards) for the dashboard.

![grafana](/assets/grafana.png)

Cheers,
Moko :)

Reference:

[https://medium.com/faun/production-grade-kubernetes-monitoring-using-prometheus-78144b835b60](https://medium.com/faun/production-grade-kubernetes-monitoring-using-prometheus-78144b835b60)
