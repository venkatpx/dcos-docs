---
post_title: Debugging
feature_maturity: experimental
menu_order: 115
---

DC/OS offers several tools to debug your services when they have failed to deploy or are not behaving as you expect. This topic goes over how to debug from both the DC/OS CLI and the DC/OS web interface.

If you do not currently have a service or pod that is either failing or not deploying, you can use the following two [Marathon application definitions](/docs/usage/marathon/application-basics/) to test the instructions in this section.

- mem-app.json

  ```json
  {
        "id": "mem-app",
        "cmd": "sleep 1000",
        "cpus": 0.1,
        "mem": 12000,
        "instances": 3,
        "constraints": [
                [
                        "hostname",
                        "UNIQUE"
                ]
        ]
  }
  ```


- stuck-sleep.json

  ```json
  {
          "id": "stuck-sleep",
          "cmd": "sleep 1000",
          "cpus": 0.1,
          "mem": 3000,
          "instances": 10,
          "constraints": [
                  [
                          "hostname",
                          "UNIQUE"
                  ]
          ]
  }
  ```
