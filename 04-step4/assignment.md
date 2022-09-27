---
slug: step4
id: cbuxjmuktww7
type: challenge
title: Application Lifecycle
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
  url: https://console-openshift-console.apps.spoke.${_SANDBOX_ID}.instruqt.io
  new_window: true
difficulty: basic
timelimit: 200
---
Connect to OpenShift again:

```
oc login -u admin -p admin https://api.crc.testing:6443 --insecure-skip-tls-verify=true
```

* `spec.statefulset.replicas: 1`
* `spec.storage.persistentVolume.size: 1Gi`
* `spec.storage.persistentVolume.storageClass: local-storage`

```yaml
apiVersion: charts.example.com/v1alpha1
kind: Cockroachdb
metadata:
  name: cockroachdb-sample
spec:
  statefulset:
    replicas: 1
  storage:
    persistentVolume:
      size: 1Gi
      storageClass: local-storage
```