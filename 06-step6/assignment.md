---
slug: step6
id: v2juyihs5qbn
type: challenge
title: Enable Application Ingress
notes:
- type: text
  contents: |-
    In the next learning module, we cover Application Ingress with ACM and the following Concepts:

    * xx
    * xx
    * xx
    * xx
    * xx

    Let's begin!
tabs:
- title: Terminal 1
  type: terminal
  hostname: container
- title: Visual Editor
  type: code
  hostname: container
  path: /root
- title: ACM Hub Console
  type: website
  url: https://multicloud-console.crc-dzk9v-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
difficulty: advanced
timelimit: 1200
---
Connect to OpenShift again:

```
oc login -u admin -p admin https://api.crc.testing:6443 --insecure-skip-tls-verify=true
```
