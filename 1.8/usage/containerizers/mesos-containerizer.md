---
nav_title: Original Mesos Containerizer
feature_maturity: 
menu_order: 0
---

The Mesos Containerizer is the original container runtime in Mesos. It does not support Docker containers, though it supports a range of isolators that can be composed to create a container. <!-- what's an isolator?? --> Refer to the [features matrix](/docs/1.8/usage/containerizers/index.md) to see if the original Mesos containerizer is the correct choice for your task.

<!-- Mesos containerizer: does not support images. Should this not be type MESOS? Therefore not a runtime? Does the mesos containerizer just package up your command into a Docker container? -->

{
  "id": "/suzanne-simple-service",
  "instances": 1,
  "container": {
    "type": "DOCKER"
  },
  "cpus": 0.1,
  "mem": 128,
  "cmd": "sleep 10"
}

- [View the Mesos docs for the Mesos containerizer](http://mesos.apache.org/documentation/latest/mesos-containerizer/).
