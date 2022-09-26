---
slug: step2
id: lcecwclx1ku7
type: challenge
title: Cluster Management
tabs:
- title: Work Terminal 1
  type: terminal
  hostname: container
- title: Hub Terminal 1
  type: terminal
  hostname: crc
- title: Spoke Terminal 3
  type: terminal
  hostname: spoke
- title: Visual Editor
  type: code
  hostname: container
  path: /root
- title: ACM Hub Console
  type: website
  url: https://multicloud-console.crc-dzk9v-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
- title: Hub Web Console
  type: website
  url: https://console-openshift-console.crc-dzk9v-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
- title: Spoke Web Console
  type: website
  url: https://console-openshift-console.apps.spoke.${_SANDBOX_ID}.instruqt.io
  new_window: true
difficulty: basic
timelimit: 8000
---
Connect to OpenShift again:

```
oc login -u admin -p admin https://api.crc.testing:6443 --insecure-skip-tls-verify=true
```

