---
post_title: Removing Agent Nodes
nav_title: Remove Node
menu_order: 801
---

You can remove agent nodes from an active DC/OS cluster. 

When you change Mesos attributes (`⁠⁠⁠⁠/var/lib/dcos/mesos-slave-common`⁠⁠⁠⁠) or resources (⁠⁠⁠⁠`/var/lib/dcos/mesos-resources`⁠⁠⁠⁠), you have to remove the agent node and re-register it with the master under a new UUID. The master will then recognize the new attributes and resources specification.

### Prerequisites:

*   DC/OS is installed using the [custom](/docs/1.9/administration/installing/custom/) installation method.
*   SSH installed and configured. This is required for accessing nodes in the DC/OS cluster.


# Define a maintenance schedule
You can define a maintenance schedule to evacuate your tasks prior to re-registering the UUID. ⁠⁠⁠All tasks that are running on the agent will be killed when you re-register the UUID. Mesos treats re-registration as a new agent.

1.  Define a maintenance schedule and then invoke the `⁠⁠⁠⁠machine/down` endpoint with a JSON definition that includes the agents. For example, [here](https://github.com/vishnu2kmohan/dcos-toolbox/blob/master/mesos/maintain-agents.sh) is a maintenance schedule and [here](https://github.com/vishnu2kmohan/dcos-toolbox/blob/master/mesos/down-agents.sh) is down agents. 

Invoking `machine/down` sends a `⁠⁠⁠⁠TASK_LOST`⁠⁠⁠⁠ message for downed tasks that were running on the agent. Some DC/OS services, for example Marathon, will relocate tasks. However some DC/OS services will not relocate tasks, for example Kafka and Cassandra.  For more information, see the DC/OS [service guides](https://docs.mesosphere.com/usage/service-guides/) and the Mesos maintenance primitives [documentation](https://mesos.apache.org/documentation/latest/maintenance/).

# Re-register the UUID

**Warning:** ⁠⁠⁠All tasks that are running on the agent will be killed since you are re-registering a UUID. Mesos treats a re-registered agent as a new agent.

1.  [SSH to the agent node](/docs/1.9/administration/access-node/sshcluster/).
1.  Stop the agent.

    -  **Private agent**
    
       ```bash
       $ sudo sh -c 'systemctl kill -s SIGUSR1 dcos-mesos-slave && systemctl stop dcos-mesos-slave
       ```
    -  **Public agent**
    
       ```bash
       $ ⁠⁠⁠⁠sudo sh -c 'systemctl kill -s SIGUSR1 dcos-mesos-slave-public && systemctl stop dcos-mesos-slave-public
       ```

1.  Reload the systemd configuration.

    ```bash
    $﻿⁠⁠⁠⁠sudo systemctl daemon-reload
    ```
    
1.  Remove the `latest` metadata pointer on the agent node:

    ```bash
    ⁠⁠⁠⁠sudo rm /var/lib/mesos/slave/meta/slaves/latest
    ```
    
1.  Start your agents with the newly configured attributes and resource specification⁠⁠.

    -  **Private agent**
    
       ```bash
       $ sudo systemctl start dcos-mesos-slave﻿⁠⁠⁠⁠
       ```﻿⁠⁠⁠⁠
       
    -  **Public agent**
    
       ```bash
       ⁠⁠⁠⁠$ sudo systemctl stop dcos-mesos-slave-public﻿⁠⁠⁠⁠
       ```