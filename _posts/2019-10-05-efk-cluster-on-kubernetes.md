---
layout: post
title: "Deploy Elasticsearch, Fluentd and Kibana on Kubernetes"
description: "Deploy EFK Stack on kubernete "
comments: false
keywords: "kubernetes, k8s, kubic, elasticsearch, fluentd, kibana"
---

## Introduction

EFK Stack or Elasticseacrh, Fluentd and Kibana is a opensource for a centralized logging solution.

This module/application on this stack is have a specific role. The role of the applications is like this:

Elasticsearch is a real-time, distributed and scalable searc engine based on apache-lucent. It's commonly used to index and search through large volumes of log data, but can also be used to search many different kinds of documents.

Usually Elasticseacrch is pairing with Logstasg, but this time i will use fluentd to collect, transform and ship log adata to elasticsearch backend. Fluentd is one of the CNCF project that graduated.

And Kibana is a visualization of the elasticsearch.

## Requirement

My environment uses 4 CPU cores and 8GB of RAM per node.

1 master nodes.
2 worker nodes.
200GB volume attached to worker nodes as a Persistent Volume.
You can use your kubernetes environment. I would suggest you use 4 CPUs and 8GB of RAM per node with 1 Master and 2 Worker or more.

Kubernetes 1.10+
kubectl client

## Deployment Guide

All of the YAML using in this posts is available at [https://github.com/sdmoko/EFK-kubernetes](https://github.com/sdmoko/EFK-kubernetes)

The steps:
1. Clone the repository on the master node

```
git clone https://github.com/sdmoko/EFK-kubernetes.git
cd EFK-kubernetes
```

2. Create a storage class, in this tutorial i'm using a local disk as a storage.
```
kubectl apply -f 00-storageClass.yaml
```

3. Create a PV. Please check and change the size of pv and values for a worker node that have a storage disk.
```
kubectl apply -f 01-pv-0.yaml
kubectl apply -f 02-pv-1.yaml
kubectl apply -f 03-pv-2.yaml
```

4. Then we need to create a namespaces for a logging system. 
```
kubectl apply -f 04-namespaces.yaml
```

5. After this create a service for elasticsearch cluster, so the Fluentd and Kibana can use it.
```
kubectl apply -f 05-elasticsearch_svc.yaml
```

6. Then create a cluster elasticsearch which use the volume that we create before.
```
kubectl apply -f 06-elasticsearch_statefulset.yaml
```

7. Then deploy Kibana and Fluentd to make it a complete logging stack. Where we can visualize the data.
```
kubectl apply -f 07-kibana.yaml
kubectl apply -f 08-fluentd.yaml
```

![Kibana Dashboard](/assets/kibana.png)

Cheers,
Moko :)

Reference:

[https://www.digitalocean.com/community/tutorials/how-to-set-up-an-elasticsearch-fluentd-and-kibana-efk-logging-stack-on-kubernetes#prerequisites](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-elasticsearch-fluentd-and-kibana-efk-logging-stack-on-kubernetes#prerequisites)

