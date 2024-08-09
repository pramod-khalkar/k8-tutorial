# K8 components

| component          | Description                                                                                        |
| ------------------ | -------------------------------------------------------------------------------------------------- |
| Cluster            | main and parent layer                                                                              |
| Node               | physical machine with CPU & memory configurations                                                  |
| Pod                | abstraction layer over container                                                                   |
| Service            | networking interface for communicating between pods                                                |
| Ingress            | main entry point for node communication                                                            |
| ConfigMap          | key value store                                                                                    |
| Secret             | similar like config map but values stored with base64 encoded                                      |
| Namespace          | logical separation wihtin cluster                                                                  |
| api server         | cluster gateway for interaction                                                                    |
| scheduler          | start and manage pods on worker nodes                                                              |
| controller manager | detect state changes of pod and recover cluster state, request scheduler for resource calclulation |
| etcd               | key value (cluster brain) to store cluster data                                                    |
| master node        | managing worker node                                                                               |
| worker node        | actual working nodes those have pods running                                                       |

# Useful commands for kubectl

| command                                                                                   | Description                                        |
| ----------------------------------------------------------------------------------------- | -------------------------------------------------- |
| `kubcetl cluster-info`                                                                    | to get the cluster information                     |
| `kubectl get pod/nodes/deployment/service/replicaset/namespaces/configmap/secret/ingress` | list the respective component mentioned in command |
| `kubectl get pod -o wide`                                                                 | get pod details along with IP address              |
| `kubectl get pod --watch`                                                                 | watch status of pod                                |
| `kubectl get all`                                                                         | to see all resources                               |
| `kubectl get deployment <deployment_name> -o yaml`                                        | get the k8 update deployment file                  |
| `kubectl create deployment <name>`                                                        | create deployment from existing                    |
| `kubectl edit deployment <depl_name>`                                                     | edit deployment file                               |
| `kubectl delete deployment <deployment_name>`                                             | delete the deployment                              |
| `kubectl logs <pod_name>`                                                                 | get the logs of pod                                |
| `kubectl describe pod <pod_name>`                                                         | to get insights of pod                             |
| `kubectl describe service <service_name>`                                                 | get service details                                |
| `kubectl exec -it <pod_name> -- bin/bash`                                                 | go inside pod terminal                             |
| `kubectl apply -f <deployment_file_name>`                                                 | create deployment from file                        |
| `kubectl delete -f <deployment_file_name>`                                                | delete with configuration file                     |
| `kubectl api-resources --namespaced=false`                                                | get the non namespaced resources                   |
| `kubectl api-resources --namespaced=true`                                                 | get the resources those are in namespace           |
| `kubectl delete validatingwebhookconfigurations`                                          | to get validating webhooks                         |

# Direct deployment commands of mongo and nginx

- `kubectl create deployment nginx-depl --image=nginx`
- `kubectl create deployment mongo-depl --image=mongo`

# Namespaces

| Name            | Description                                                                                                           |
| --------------- | --------------------------------------------------------------------------------------------------------------------- |
| default         | the resources you create locates here using 'kubectl create namespaces <name_of_namespace>' or with config (yaml)file |
| kube-node-lease | maintain the information of each node with lease object (heart beat of node)                                          |
| kube-public     | public available info, config map with cluster info which we get by `kubectl cluster-info`                            |
| kube-system     | contains system, master, kubctl process (DO NOT MODIFY)                                                               |

- configMap and secretConfig limited to indiviual namespace cant share

- services can be shared across namespaces

- Vol & node are at cluster level cant be created in namespaces

- If you dont pass namespace it will create in default namespace

- If you want to avoid every time passing `-n <ns>` then use `kubens <ns_name` and `kubens` to see active ns. to install `brew install kubectx`

##### Check mongo application

[Mongo application](./mongo/README.md)

##### How to troubleshoot

[Troubleshoot guide](./troubleshoot.md)
