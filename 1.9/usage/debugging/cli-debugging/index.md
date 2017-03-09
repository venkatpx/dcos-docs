---
post_title: Debugging from the DC/OS CLI
menu_order: 10
---

The DC/OS CLI offers a number of commands to debug services that are not deploying or not behaving as expected.

To see full logs, run any DC/OS CLI command with `--log-level=debug`. For instance, to troubleshoot HDFS package installation, use `dcos -—log-level="debug" package install hdfs`. For more information about log levels, consult the [CLI command reference](/docs/1.9/usage/cli/command-reference/) or run `dcos --help`.
