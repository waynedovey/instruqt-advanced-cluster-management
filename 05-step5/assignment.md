---
slug: step5
id: sctxdux1axjs
type: challenge
title: Advanced Policy Management
notes:
- type: text
  contents: |-
    In the next learning module, we cover Advanced Policy Management with ACM and the following Concepts:

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
- title: Web Console
  type: website
  url: https://console-openshift-console.apps.spoke.${_SANDBOX_ID}.instruqt.io
  new_window: true
difficulty: basic
timelimit: 600
---
Connect to ACM Hub:

```
oc login -u admin -p admin https://api.crc.testing:6443 --insecure-skip-tls-verify=true
```

### Prerequisites

Some of the policies presented in the repository apply on the mariadb application. In order to deploy the application, run the next command on the hub cluster.

```
oc apply -f content/application.yml
```

The policies in this repository are deployed in the rhacm-policies namespace. Deploying the namespace can be done by running the next command on the hub cluster.

```
oc apply -f content/namespace.yml
```

The policies in this repository are using a PlacementRule resource that maps policies to managed clusters with the 'prod' tag assigned to them. In order to deploy the PlacementRule resource, run the next command on the hub cluster.

```
oc apply -f content/placementrule.yml
```

##