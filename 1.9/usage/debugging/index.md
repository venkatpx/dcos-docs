---
post_title: Debugging
feature_maturity: experimental
menu_order: 115
---

DC/OS offers several tools to debug your services when they have failed to deploy or are not behaving as you expect. This topic goes over how to debug from both the DC/OS CLI and the DC/OS web interface.

If you do not currently have a failing service or pod, you can deploy the following two [Marathon application definitions](/docs/usage/marathon/application-basics/) to test the instructions in this section.

- (mem-app.json)[/docs/1.9/usage/debugging/mem-app.json]
- (stuck-sleep.json)[/docs/1.9/usage/debugging/stuck-sleep.json]
