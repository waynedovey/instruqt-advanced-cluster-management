---
slug: step2
id: ke9ivfcglspb
type: challenge
title: Cluster Management
tabs:
- title: Work Terminal 1
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
- title: Hub Web Console
  type: website
  url: https://console-openshift-console.crc-dzk9v-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
difficulty: advanced
timelimit: 8000
---
Connect to OpenShift again:

```
oc login -u admin -p admin https://api.crc.testing:6443 --insecure-skip-tls-verify=true
```

Start the Import for spoke1 Cluster
```
export CLUSTER_NAME=spoke1
```

```
oc new-project ${CLUSTER_NAME}
```

```
oc label namespace ${CLUSTER_NAME} cluster.open-cluster-management.io/managedCluster=${CLUSTER_NAME}
```

```
cat <<EOF | oc apply -n ${CLUSTER_NAME} -f -
apiVersion: cluster.open-cluster-management.io/v1
kind: ManagedCluster
metadata:
  name: ${CLUSTER_NAME}
spec:
  hubAcceptsClient: true
EOF
```

```
cat <<EOF | oc apply -n ${CLUSTER_NAME} -f -
apiVersion: agent.open-cluster-management.io/v1
kind: KlusterletAddonConfig
metadata:
  name: ${CLUSTER_NAME}
  namespace: ${CLUSTER_NAME}
spec:
  clusterName: ${CLUSTER_NAME}
  clusterNamespace: ${CLUSTER_NAME}
  applicationManager:
    enabled: true
  certPolicyController:
    enabled: true
  clusterLabels:
    cloud: auto-detect
    vendor: auto-detect
  iamPolicyController:
    enabled: true
  policyController:
    enabled: true
  searchCollector:
    enabled: true
EOF
```

```
oc get secret ${CLUSTER_NAME}-import -n ${CLUSTER_NAME} -o jsonpath={.data.crds\\.yaml} | base64 --decode > /root/${CLUSTER_NAME}-klusterlet-crd.yaml
```

```
oc get secret ${CLUSTER_NAME}-import -n ${CLUSTER_NAME} -o jsonpath={.data.import\\.yaml} | base64 --decode > /root/${CLUSTER_NAME}-import.yaml
```

```
oc login --token=superSecur3T0ken --server=http://${CLUSTER_NAME}:8001
```

```
kubectl apply -f /root/${CLUSTER_NAME}-klusterlet-crd.yaml
```

```
kubectl apply -f /root/${CLUSTER_NAME}-import.yaml
```

Start the Import for spoke2 Cluster

```
oc login -u admin -p admin https://api.crc.testing:6443 --insecure-skip-tls-verify=true
```


```
export CLUSTER_NAME=spoke2
```

```
oc new-project ${CLUSTER_NAME}
```

```
oc label namespace ${CLUSTER_NAME} cluster.open-cluster-management.io/managedCluster=${CLUSTER_NAME}
```

```
cat <<EOF | oc apply -n ${CLUSTER_NAME} -f -
apiVersion: cluster.open-cluster-management.io/v1
kind: ManagedCluster
metadata:
  name: ${CLUSTER_NAME}
spec:
  hubAcceptsClient: true
EOF
```

```
cat <<EOF | oc apply -n ${CLUSTER_NAME} -f -
apiVersion: agent.open-cluster-management.io/v1
kind: KlusterletAddonConfig
metadata:
  name: ${CLUSTER_NAME}
  namespace: ${CLUSTER_NAME}
spec:
  clusterName: ${CLUSTER_NAME}
  clusterNamespace: ${CLUSTER_NAME}
  applicationManager:
    enabled: true
  certPolicyController:
    enabled: true
  clusterLabels:
    cloud: auto-detect
    vendor: auto-detect
  iamPolicyController:
    enabled: true
  policyController:
    enabled: true
  searchCollector:
    enabled: true
EOF
```

```
oc get secret ${CLUSTER_NAME}-import -n ${CLUSTER_NAME} -o jsonpath={.data.crds\\.yaml} | base64 --decode > /root/${CLUSTER_NAME}-klusterlet-crd.yaml
```

```
oc get secret ${CLUSTER_NAME}-import -n ${CLUSTER_NAME} -o jsonpath={.data.import\\.yaml} | base64 --decode > /root/${CLUSTER_NAME}-import.yaml
```

```
oc login --token=superSecur3T0ken --server=http://${CLUSTER_NAME}:8001
```

```
kubectl apply -f /root/${CLUSTER_NAME}-klusterlet-crd.yaml
```

```
kubectl apply -f /root/${CLUSTER_NAME}-import.yaml
```

Validate both Clusters are imported

```
oc login -u admin -p admin https://api.crc.testing:6443 --insecure-skip-tls-verify=true
```

```
cm get clusters
```

