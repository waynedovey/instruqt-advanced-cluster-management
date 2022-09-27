---
slug: step3
id: rxvyboh3ivt3
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

Label the Clusters to ensure Application placement rules

```
export CLUSTER_NAME=spoke1
```

```
oc label managedclusters ${CLUSTER_NAME} "environment=dev" --overwrite
```

```
export CLUSTER_NAME=spoke2
```

```
oc label managedclusters ${CLUSTER_NAME} "environment=dev" --overwrite
```

Clone the test applicaton

```
git clone https://github.com/waynedovey/blue-green-rhacm.git
```

```
cd blue-green-rhacm
```

Create and Deploy the Application

```
./acm-create.sh
````