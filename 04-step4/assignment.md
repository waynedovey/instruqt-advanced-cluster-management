---
slug: step4
id: kiyiwsdbpyod
type: challenge
title: Governance, Risk and Compliance
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
- title: Hub OCP Console
  type: website
  url: https://console-openshift-console.crc-dzk9v-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
difficulty: advanced
timelimit: 600
---
Connect to ACM Hub:
```
oc login -u admin -p admin https://api.crc.testing:6443 --insecure-skip-tls-verify=true
```

Download the first policy for namespace Creation

```
curl -s https://raw.githubusercontent.com/stolostron/policy-collection/main/stable/CM-Configuration-Management/policy-namespace.yaml -o policy-namespace.yaml
```

Modify the Policy policy-namespace.yaml in the "Visual Editor".

Change the environment from "dev"
```
---
apiVersion: apps.open-cluster-management.io/v1
kind: PlacementRule
metadata:
  name: placement-policy-namespace
spec:
  clusterConditions:
  - status: "True"
    type: ManagedClusterConditionAvailable
  clusterSelector:
    matchExpressions:
      - {key: environment, operator: In, values: ["dev"]}
```

To "prod" to match the cluster labels
```
---
apiVersion: apps.open-cluster-management.io/v1
kind: PlacementRule
metadata:
  name: placement-policy-namespace
spec:
  clusterConditions:
  - status: "True"
    type: ManagedClusterConditionAvailable
  clusterSelector:
    matchExpressions:
      - {key: environment, operator: In, values: ["prod"]}
```

Review the Policy and save

Apply the Policy in the default namespace
```
oc apply -f policy-namespace.yaml -n default
```


Verify the Policy has worked against both clusters
```
export CLUSTER_NAME=spoke1
```
```
oc login --token=superSecur3T0ken --server=http://${CLUSTER_NAME}:8001
```

Display the newly created namespace
```
kubectl get namespaces
```
```
export CLUSTER_NAME=spoke2
```
```
oc login --token=superSecur3T0ken --server=http://${CLUSTER_NAME}:8001
```
Display the newly created namespace
```
kubectl get namespaces
```

Next Download the second policy

```
curl -s https://raw.githubusercontent.com/stolostron/policy-collection/main/stable/CM-Configuration-Management/policy-pod.yaml -o policy-pod.yaml
```
Modify the Policy ^^policy-pod.yaml^^ in the "Visual Editor".

Add the new "namespace" value created in the previous step

```
          object-templates:
            - complianceType: musthave
              objectDefinition:
                apiVersion: v1
                kind: Pod # nginx pod must exist
                metadata:
                  name: sample-nginx-pod
                  namespace: prod
                spec:
                  containers:
                  - image: nginx:1.18.0
                    name: nginx
                    ports:
                    - containerPort: 80
```

Next, change the Placement rule again to allow this to propagate to the Prod Clusters as before

```
---
apiVersion: apps.open-cluster-management.io/v1
kind: PlacementRule
metadata:
  name: placement-policy-pod
spec:
  clusterConditions:
  - status: "True"
    type: ManagedClusterConditionAvailable
  clusterSelector:
    matchExpressions:
      - {key: environment, operator: In, values: ["prod"]}
```

Connect to ACM Hub:
```
oc login -u admin -p admin https://api.crc.testing:6443 --insecure-skip-tls-verify=true
```

Apply the Policy in the default namespace
```
oc apply -f policy-pod.yaml -n default
```

Validate the new pods are running in correct namespace on both Clusters
```
export CLUSTER_NAME=spoke1
```
```
oc login --token=superSecur3T0ken --server=http://${CLUSTER_NAME}:8001
```

Display the newly pods in the prod namespace
```
kubectl get pods -n prod
```
```
export CLUSTER_NAME=spoke2
```
```
oc login --token=superSecur3T0ken --server=http://${CLUSTER_NAME}:8001
```
Display the newly pods in the prod namespace
```
kubectl get pods -n prod
```

Note, both **oc** and **kubectl** commands can be used interchangeably

Completed, move onto the next assignment.