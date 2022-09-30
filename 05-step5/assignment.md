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
- title: ACM Hub Console
  type: website
  url: https://multicloud-console.crc-dzk9v-master-0.crc.${_SANDBOX_ID}.instruqt.io
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
curl -s https://raw.githubusercontent.com/waynedovey/instruqt-advanced-cluster-management/main/05-step5/content/application.yml -o application.yml
```
```
oc apply -f application.yml
```

The policies in this repository are deployed in the rhacm-policies namespace. Deploying the namespace can be done by running the next command on the hub cluster.

```
curl -s https://raw.githubusercontent.com/waynedovey/instruqt-advanced-cluster-management/main/05-step5/content/namespace.yml -o namespace.yml
```
```
oc apply -f namespace.yml
```

The policies in this repository are using a PlacementRule resource that maps policies to managed clusters with the 'prod' tag assigned to them. In order to deploy the PlacementRule resource, run the next command on the hub cluster.

```
curl -s https://raw.githubusercontent.com/waynedovey/instruqt-advanced-cluster-management/main/05-step5/content/placementrule.yml -o placementrule.yml
```
```
oc apply -f placementrule.yml
```

In this section we will start enforcing a range of Policies. This is to ensure we have a locked down namespace.
These can be namespace or clusterwide:

# Firstly we implement LimitRange:

```
curl -s https://raw.githubusercontent.com/waynedovey/instruqt-advanced-cluster-management/main/05-step5/content/limitrange-policy.yml -o limitrange-policy.yml
```
```
oc apply -f limitrange-policy.yml
```

Display the newly pods in the prod namespace on spoke1

```
export CLUSTER_NAME=spoke1
```
```
oc login --token=superSecur3T0ken --server=http://${CLUSTER_NAME}:8001
```

Display the newly pods in the prod namespace
```
kubectl describe LimitRange -n mariadb
```

Display the newly pods in the prod namespace on spoke2

```
export CLUSTER_NAME=spoke2
```
```
oc login --token=superSecur3T0ken --server=http://${CLUSTER_NAME}:8001
```

Display the newly pods in the prod namespace
```
kubectl describe LimitRange -n mariadb
```