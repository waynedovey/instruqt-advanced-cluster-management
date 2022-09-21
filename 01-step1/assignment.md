---
slug: step1
id: odx020nssccy
type: challenge
title: Enable ACM
notes:
- type: text
  contents: |-
    In this learning module, we cover enabling ACM and the following Concepts:

    * Create the required Namespace.
    * Install the ACM Operator.
    * Provision the Custom Resource.
    * Access the ACM console.

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
timelimit: 800
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

Wait until the Subscription is Installed:

```
oc get csv
```

The Phase should change from "Installing" to Succeeded"


Finally enable the Custom Resource:

```
oc create -f https://raw.githubusercontent.com/waynedovey/instruqt-advanced-cluster-management/main/01-step1/content/custom-resource.yaml
```

Check for the status of the Operator Installation (Can take up to 10min):

```
echo $(oc get mch -o=jsonpath='{.items[0].status.phase}')
````

The Status should change from "Installing" to Runnng"

Get the Route for the ACM Service and Navigate to this:

Login with admin/admin

```
echo https://$(oc get route | awk '{print $2}' | grep -v HOST)
```