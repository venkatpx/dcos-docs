---
post_title: DC/OS API Reference
nav_title: API Reference
menu_order: 4
---

The DC/OS API is a collection of routes backed by [DC/OS components](/docs/1.9/overview/architecture/components/) that are made available through an API gateway called the [Admin Router](/docs/1.9/overview/architecture/components/#admin-router).


## Admin Router

Admin Router is an API gateway built on top of NGINX.

Admin Router exposes four types of routes:

- **Proxy Routes** retrieve resources from another address.
- **File Routes** retrieve static files.
- **Redirect Routes** redirect to another address.
- **Rewrite Routes** translate routes into other routes.

Admin Router uses these route types to accomplish four primary goals:

- Present a unified control plane for the DC/OS API
- Proxy API requests to component services on master and agent nodes
- Enforce user authentication
- Serve up the DC/OS GUI


## Cluster Access

To determine the address of your cluster, see [Cluster Access](/docs/1.9/api/access/).


## Route Topology

There are two varieties of Admin Router:

- **Admin Router Master** runs on each master node and serves as the primary API gateway for interaction with DC/OS components.

  See [Master Routes](/docs/1.9/api/master-routes/) for a list of routes available on master nodes.

- **Admin Router Agent** runs on each agent node and provides routes for monitoring, debugging, and administration.

  Some agent routes, like logs and metrics, are proxied through the master Admin Router to allow external access.
Other routes, like component management, are for internal use only.

  See [Agent Routes](/docs/1.9/api/agent-routes/) for a list of routes available on agent nodes.

![DC/OS API Routing](/docs/1.9/api/img/dcos-api-routing.png)
