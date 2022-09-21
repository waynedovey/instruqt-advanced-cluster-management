---
slug: step1
id: odx020nssccy
type: challenge
title: Enable ACM
notes:
- type: text
  contents: |-
    In this learning module, we covered how to easily create the following types of Operators with the Operator SDK:

    * Scale horizontally.
    * Survive disk, machine, rack, and even datacenter failures with minimal latency disruption and no manual intervention.
    * Supports strongly-consistent ACID transactions and provides a familiar SQL API for structuring, manipulating, and querying data.

    Let's begin!
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
Let's begin by connecting to OpenShift:

```
oc login -u admin -p admin https://api.crc.testing:6443 --insecure-skip-tls-verify=true
```

Create a new namespace called `open-cluster-management`:

```
oc create namespace open-cluster-management
```

Switch to new namespace called `open-cluster-management`:

```
oc project open-cluster-management
```

Let's now create the OperatorGroup for ACM:

```
oc create -f https://raw.githubusercontent.com/waynedovey/instruqt-advanced-cluster-management/main/01-step1/content/operator-group.yaml
```

Then create the Subscription:

```
oc create -f https://raw.githubusercontent.com/waynedovey/instruqt-advanced-cluster-management/main/01-step1/content/acm-operator-subscription.yaml
```

Finally enable the Custom Resource:

```
oc create -f https://raw.githubusercontent.com/waynedovey/instruqt-advanced-cluster-management/main/01-step1/content/acm-operator-subscription.yaml
```