---
author: "Wren Howell"
title: "Understanding K8 "
date: 2025-04-10
description: "k8"
tags: ["K8, threats"]
thumbnail: https://i.imgur.com/0HhNox3.png
---

Kubernetes is a technology that most people and most organizations do not understand. There is a lot of "deploy and hope" in most organizations. Kubernetes deployment is messy, and Kubernetes has a lot of moving parts that make it difficult to understand. So in this post, I want to break down the essential parts of Kubernetes and introduce how k8 clusters can be compromised.

## What is Kubernetes?

Kubernetes, often abbreviated as **k8s**, is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications.

## So what does this mean, and what problem did it solve?

When a developer deployed an app on a container, they had to manually start, stop, and manage containers across multiple machines. For example, if an application needed more memory to run, a developer had to stop the container, increase the memory, and then restart it manually. For a small number of containers this might be okay, but this quickly becomes unmanageable when there are hundreds of containers to manage. Kubernetes was a technology developed by Google to help automate this process.

## Kubernetes Architecture

Kubernetes architecture is made up of three core parts: the control plane, the worker node, and the pod.

### Control Plane

The control plane is the brain of Kubernetes. It consists of:

- **API Server**: The interface that runs the Kubernetes API and where all communication happens.
- **etcd**: The database that stores the state of the cluster.
- **Scheduler**: The process that assigns pods to nodes based on resource availability and constraints.

### Worker Node

A worker node is a virtual machine on which pods run. Each worker node has:

- **Kubelet**: The agent that communicates back to the k8s control plane.
- **KubeProxy**: Manages networking rules and load balancing between services.
- **Container Runtime**: Kubernetes supports multiple runtimes; containerd is the most widely used default, while CRI-O is another supported option.

### Pod

A pod is the smallest deployable unit in Kubernetes and can contain one or more containers.

## The Airport Analogy

This can be a little confusing, so let's break it down using an airport as an example.

The airport management staff and air traffic control are like k8s's control plane. It is responsible for organizing flights, scheduling, and maintaining overall operations.

- The **control tower** is like the **API Server**: it receives flight plans and coordinates with pilots on when to land and take off.
- The **flight scheduler** is like the **Scheduler**: it assigns gates and runways for each flight.
- The **flight database** is like **etcd**: it stores all schedules and aircraft status.

A **worker node** is where all the action happens. Each worker node is like a terminal or runway where flights arrive, depart, and park.

- The **flight attendants** are like the **Kubelet**: they ensure passengers follow instructions so flights operate safely.
- The **engines, wings, and landing gear** are like the **Container Runtime**: the tools that ensure the plane can actually fly.
- The **check-in and baggage staff** are like **KubeProxy**: they handle communication and routing between services.

## Deployment Types

### Managed Kubernetes

Managed Kubernetes instances are hosted by a cloud service provider like GCP, Azure, or AWS. The cloud provider configures, provisions, and maintains the k8s clusters, allowing organizations to delegate updates, infrastructure provisioning, and ongoing management.

### Unmanaged Kubernetes Clusters

In unmanaged clusters, the user is responsible for installing, deploying, and operating the Kubernetes environment on infrastructure they control. This gives organizations more control but requires more hands-on management.

### Hybrid Kubernetes Clusters

A hybrid deployment combines on-premises servers, private cloud, and public cloud providers in a k8s environment.

## Kubernetes Attacks

Kubernetes attacks typically begin at the pod level. Common entry points include:

- A threat actor compromising the application running inside a pod.
- A threat actor phishing a user who has access to a pod.
- A threat actor escalating privileges from within a pod to gain broader cluster access.

From there, attackers may attempt to move laterally across nodes, access the API server, extract secrets from etcd, or gain cluster-admin privileges. Understanding the architecture above is essential to recognizing where those attack paths exist.

{{< css.inline >}}

<style>
.emojify {
	font-family: Apple Color Emoji, Segoe UI Emoji, NotoColorEmoji, Segoe UI Symbol, Android Emoji, EmojiSymbols;
	font-size: 2rem;
	vertical-align: middle;
}
@media screen and (max-width:650px) {
  .nowrap {
    display: block;
    margin: 25px 0;
  }
}
{{ $image := $resource.Fit "600x400" }}
</style>

{{< /css.inline >}}
