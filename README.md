# Kubernetes-notes

Simplified Kubernetes Architecture Components Explained :- 
======================================================

This document explains the key components that make up the architecture of a Kubernetes cluster, in simple terms

Table of Contents
=================

    Control Plane (Master Node Components)
    Worker Node Components
    Other Components


![kubernetes-Architecture](https://github.com/DineshA055/Kubernetes-notes/assets/101075223/2077d0cc-92a6-43ea-b8e0-e97b22f7289b)

    

Kubernetes Architecture Diagram
=======================================
Control Plane (Master Node Components)
========================================


Kubernetes architecure broken down into two parts control plane and data plane has worker node

Control plane includes   -> {Kube-controller-manager}    {etcd}   {kube-apiserver}    {kube-scheduler}

Node (data plane )     ->   includes {kubelet}     {kube-proxy}     {Container-Run-time}

Control plane provides core kubernetes services and Orchestration of all application workloads and while actuall application workload run on the Node components 

In cloud patform control plane is automatically created / configured  / managed by cloud platform 

Four main service runnning in control plane 


1. Kube-api-server   = [ how the underline api's are exposed and this components provide the interaction for management tools such as "kubectl" ]

   
   
2. ETCD    = [ Maintains the state of the kubernetes cluster and its configurations, higly available service , key-value store with kubernetes ]


   
3. Kube-controller-manager = [ Oversees smaller number of controllers manager that perform actions such has replicating pods and handling node            operations ]

   
4. kube-scheduler = [when you create or scale a applications kube-scheduler determines what node to run the workload and when it should start there]



   
 WokerNode [data-plane]



1.Kublet = [ kubelet is kubernetes agent and process orchestration request from the controller plane and schedule the requested containers ]



2.kubeproxy = [ Virtual network is handled by kube-proxy in each node and proxy routes network traffic and manages IP addresses for srevices and pods]



3. Container-Runtime = [ Conatiner runtime is the component allows containerized applications to run and interact with additional resources such has virtual network and storage ] 



LET SEE HOW KUBERNETES CLUSTER INSIDE NODE WORKS EACH OHER SHARING REQUEST AND PERFORM ACTIONS ☑️
Architure well defined














step 1:- A kubectl gives a pod deployment manifest to API Server   -----> and then api server creates a deployment resource--------that information stored and saved in ETCD 
step2:- Deployment controller watches for any new deployment resource create replicaset resource 
step3:- Replicaset controller watches for any new replicaset resources -------replicaset controller creates the pods resource based on how many replicaset and actual pods are present    
step4 :- Kubescheduler watches for unbond pod resources and schedule them on target node
step5:- Kubelet calls container runtime interface and container network interface to create a pod in container with networking configured
step6:- CRI (container runtime interface ) calls host compute layer (HCL) to create container and host networking service called (HNS) to create the endpoint
step7:- Kube-proxy wataches for any new endpoint and program HNS with load balancer and access control list



API SEREVER
===========

This is the "front desk" of Kubernetes. Whenever you want to interact with your cluster, your request goes through the API Server. It validates and processes these requests to the backend components.


ETCD
=====
Think of this as the "database" of Kubernetes. It stores all the information about your cluster—what nodes are part of the cluster, what pods are running, what their statuses are, and more.

SCHEDULER
=========
The "event planner" for your containers. When you ask for a container to be run, the Scheduler decides which machine (Node) in your cluster should run it. It considers resource availability and other constraints while making this decision.

CONTROLLER MANAGER
==================
Imagine a bunch of small robots that continuously monitor the cluster to make sure everything is running smoothly. If something goes wrong (e.g., a Pod crashes), they work to fix it, ensuring the cluster state matches your desired state.

CLOUD CONTROL MANAGER
=====================
This is a specialized component that allows Kubernetes to interact with the underlying cloud provider, like AWS or Azure. It helps in tasks like setting up load balancers and persistent storage.

==============================================
WORKER NODE COMPONENETS
==============================================
KUBELET
=======
This is the "manager" for each worker node. It ensures all containers on the node are healthy and running as they should be.

KUBE-PROXY
==========

Think of this as the "traffic cop" for network communication either between Pods or from external clients to Pods. It helps in routing the network traffic appropriately.

Container Runtime
==================
This is the software used to run containers. Docker is commonly used, but other runtimes like containerd can also be used.

Other Components:-
================
Pod
=====
The smallest unit in Kubernetes, a Pod is a group of one or more containers. Think of it like an apartment in an apartment building.

SERVICE
=======

This is like a phone directory for Pods. Since Pods can come and go, a Service provides has a stable "address" so that other parts of your application can find them.

Volume
=======
This is like an external hard-drive that can be attached to a Pod to store data.

Namespace
=========
A way to divide cluster resources among multiple users or teams. Think of it as having different folders on a shared computer, where each team can only see their own folder.

Ingress
=======
Think of this as the "front door" for external access to your applications, controlling how HTTP and HTTPS traffic should be routed to your services.

And there you have it! That's a simplified breakdown of Kubernetes architecture components.

