---
layout: post
title: "Create Kubernetes Cluster with Kubic"
description: "Create a simple Kubernetes Cluster with Kubic"
comments: false
keywords: "kubernetes, k8s, kubic, openSUSE"
---

## What is openSUSE Kubic?

openSUSE Kubic is a Certified Kubernetes distribution & container-related technologies built by the openSUSE community.

## What is kubeadm?

kubeadm is a toolkit produced by Kubernetes upstream for the creation and upgrade of Kubernetes clusters

## What is Kubernetes?

Kubernetes is an open-source system for automating deployment, scaling, and management of containerised applications. It groups containers that make up an application into logical units for easy management and discovery. Services then receive features like self-healing, high-availability, and load balancing with Kubernetes taking steps to ensure services keep running even in the event of failures. Kubernetes builds upon 15 years of experience of running production workloads at Google, combined with best-of-breed ideas and practices from the community.

Put simply, if you want to run containers across multiple servers in a coordinated way, you probably want to use Kubernetes.

On openSUSE Tumbleweed MicroOS Kubic, by default the container runtime is CRI-O/Podman. 

##Clustering Kubernetes with Kubic

Because i'm using cloud images openstack for Kubic, i'll not tell about how to install a openSUSE MicroOS Kubic. I'll go to step for clustering kubernetes.

The steps:
1. We need to init the master node. The command we need to run is.

```
kubeadm init --pod-network-cidr=10.244.0.0/16
```

Parameter `--pod-network-cidr=10.244.0.0/26` is for setting up a recommended CNI in Kubic, which is using `flannel`.

2. Configure user to be able to talk to cluster by running command
```
mkdir -p ~/.kube
cp -i /etc/kubernetes/admin.conf ~/.kube/config
```

3. Setting up the network plugin. There is yaml available in Kubic for kubernetes. The yaml is located at `/usr/share/k8s-yaml/`. Running this command to setting ip CNI flannel
```
kubectl apply -f /usr/share/k8s-yaml/flannel/kube-flannel.yaml
```

4. Join nodes to cluster. First, generate a token for joining the node to cluster with command
```
kubeadm token create --print-join-command
```
Example of the output of command
```
kubic-master:~ # kubeadm token create --print-join-command
kubeadm join 10.0.0.18:6443 --token u0hkpv.ii1sh7eklc3frivp     --discovery-token-ca-cert-hash sha256:6be6a61c71e0fcb91271689911e51709fbf008ff00b8314eb2f08bdccf765eb8 
```

5. Run join command on the nodes. Example the command:
```
kubic-master:~ # kubeadm token create --print-join-command
kubeadm join 10.0.0.18:6443 --token u0hkpv.ii1sh7eklc3frivp     --discovery-token-ca-cert-hash sha256:6be6a61c71e0fcb91271689911e51709fbf008ff00b8314eb2f08bdccf765eb8 
```
You need to change the token and ca-hash with your own token and ca-hash.


6. Verify the cluster and node
```
kubectl get nodes
```
Example of the output
```
kubic-master:~ # kubectl get nodes
NAME             STATUS   ROLES    AGE    VERSION
kubic-master     Ready    master   2d6h   v1.15.4
kubic-worker-1   Ready    <none>   2d6h   v1.15.4
kubic-worker-2   Ready    <none>   2d6h   v1.15.4
```

Cheers,
Moko :)

Reference:
https://en.opensuse.org/Kubic:kubeadm

