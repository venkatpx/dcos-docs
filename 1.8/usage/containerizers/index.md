---
nav_title: Using Containerizers
menu_order: 40
---

Containerizers allow you to run tasks in containers. Running tasks in containers offers a number of benefits, including the ability to isolate tasks from one another and control task resources programmatically.

DC/OS supports the Mesos containerizer types :

- The [original Mesos containerizer](/docs/1.8/usage/containerizers/mesos-containerizer/).

- The [DC/OS Universal Container Runtime](/docs/1.8/usage/containerizers/ucr/)

- The [Docker containerizer](/docs/1.8/usage/containerizers/docker-containerizer/).

The tables below provide a feature comparison of your containerizer choices on DC/OS.

## DC/OS Features

| 																				| Docker			| Original Mesos				| UCR 			| Comments |
| --------------------------------------- | ----------- | --------------------- | --------- | -------- |
| **Container Images** 										| Yes					| No										| Yes				|					 |
| **Docker Containers** 									| Yes					| No										| Yes				|					 |
| **Pods**																| No					| No										| Yes				|					 |
| **GPUs**																| No					| No										| Yes				|					 |
| **DC/OS CLI**														| No					| Yes										| Yes				|					 |
| **URIs**																| Yes					| Yes										| Yes				|					 |
| **Runtime Privileges**									| Yes					| No										| No				|					 |
| **Docker Options**											| Yes					| No										| No				|					 |
| **Force Pull**													| Yes					| No										| No				|					 |
| **Secrets**															| Yes					| Yes										| Yes				| Enterprise only |
| **Debugging (from DC/OS CLI??)**				| No					| Yes										| Yes				|					 |
| **[Health Checks](link)**								| Yes					| Yes										| Yes				|					 |
| **All Security Modes**									| Yes					| Yes										| Yes				| Enterprise only |

## Storage

|																					|	Docker			|	Original Mesos				|	UCR				|Comments |
| --------------------------------------- | ----------- | --------------------- | --------- | --------- |
| **Ephemeral Volumes**  									|	Yes					| Yes										| Yes				|						|
| **Local Persistent Volumes**						| Yes					| Yes										| Yes				|						|
| **Host Volumes**												| Yes					| Yes 									| Yes				| not in UI |

## Service Endpoints

|																					|	Docker			|	Original Mesos				|	UCR				|Comments   |
| --------------------------------------- | ----------- | --------------------- | --------- | --------- |
| **Named Ports**													| No					| No										| No				|						|
| **Numbered Ports**											| Yes					| No										| No				|						|
| **Layer 4 Load Balancer**								| Yes					| Yes										| Yes				| Requires defined service endpoints, TCP health checks do not work with L4LB |

## Networking

|																					|	Docker			|	Original Mesos				|	UCR				|Comments   |
| --------------------------------------- | ----------- | --------------------- | --------- | --------- |
| **[Host Networking](link)**							| Yes					| Yes										| Yes				|						|
| **[Bridge Networking](link)**						| Yes					| No										| No				|						|
| **[CNI](link?)**												| No					| Yes										| Yes				|						|
| **[Virtual Network](link)**							| Yes					| Yes										| Yes				| Docker 1.11+ |
| **Port Mapping**												| Yes					| No										| No				|						|

## Private Registry

|																					|	Docker			|	Original Mesos				|	UCR				|
| --------------------------------------- | ----------- | --------------------- | --------- |
| **Private Registry (Container Auth)**		| Yes					| No										| No				|
| **Private Registry (Cluster Auth)**			| No					| No										| Yes				|
