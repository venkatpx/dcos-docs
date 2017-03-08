---
post_title: Stuck Deployments
feature_maturity: experimental
menu_order: 0
---

# How Offer Matching Works

DC/OS services or pods often fail to deploy because the resource offers from Mesos do not match or cannot match the resources the service or pod requests in the [Marathon application definition](/docs/1.9/usage/marathon/application-basics/)). Below is an overview of the offer matching process.

1. You post an application or pod definition to Marathon either via the DC/OS CLI (`dcos marathon app add <my-service>.json`) or the DC/OS web interface. The service specifies resource requirements and/or placement constraints as well as the number of instances to launch.

1. Marathon adds the new service or pod to the launch queue.

1. Every 5 seconds (by default), Mesos sends one offer per agent.

1. For each reseource offer, Marathon checks if there is a service or pod in the launch queue whose requirements all match the offer. If Marathon finds a service or pod whose requirements and constraints match the offer, Marathon will launch the service or pod.

1. If an offer never arrives that match a service or pod's requirements and constraints, Marathon will not be able to launch the application.

If there is never an offer showing up containing for example 100cpus, marathon will not be able to launch this application requesting 100cpus, because it does not fit inside the given offer.

# Why Your Service or Pod is Stuck

There are several reasons why your service or pod may fail to deploy. Some possibilities include:

- Marathon isn't getting the resource offers it needs to launch the app.
  Use the [CLI](/docs/1.9/usage/debugging/cli-debugging) debug subcommands or the [debugging page in the DC/OS web interface](/docs/1.9/usage/debugging/gui-debugging) to troubleshoot unmatched or unaccepted resource offers from Mesos. You can also [consult the service and task logs](/docs/1.9/administration/logging/).

- The service's health check is failing.
  If a service has a health check, deployment does not complete until the health check passes. You can see the health of a service with Marathon health checks from [the DC/OS web interface](/docs/1.9/usage/debugging/gui-debugging). To see more information about the health of a service with Marathon health checks, run `dcos marathon app list --json` from the DC/OS CLI.

- `docker pull` is failing.
  If your app runs in a Docker image, the Mesos agent node will first have to pull the Docker image. If this fails, your app could get stuck in a "deploying" state. The Mesos agent logs (`<dcos-url>/mesos/#/agents/`) will contain this information. You will see an error in the log similar to the following.

  ```
  6b50d4f5-05d6-4b99-bb63-115d5acd2aca-0000 failed to start: Failed to run 'docker -H unix:///var/run/docker.sock pull /mybadimage/fakeimage:latest': exited with status 1; stderr='Error parsing reference: "/mybadimage/fakeimage:latest" is not a valid repository/tag
  ```

- Your application or application group definition is otherwise badly configured.
The DC/OS web interface performs some validation of Marathon application and pod definitions. You can also use the [marathon-validate](https://github.com/dcos-labs/marathon-validate) script to validate your app or group definition locally, before you deploy it to DC/OS.
