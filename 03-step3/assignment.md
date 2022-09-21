---
slug: step3
id: dy7ocj2eyokq
type: challenge
title: Apply the CockroachDB Custom Resource Definition
tabs:
- title: Terminal 1
  type: terminal
  hostname: container
- title: Visual Editor
  type: code
  hostname: container
  path: /root
- title: Web Console
  type: website
  url: https://console-openshift-console.crc-dzk9v-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
difficulty: basic
timelimit: 200
---
Connect to OpenShift again:

```
oc login -u admin -p admin https://api.crc.testing:6443 --insecure-skip-tls-verify=true
```

```
