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

# Direct deployment commands

`kubectl create deployment nginx-depl --image=nginx`
`kubectl create deployment mongo-depl --image=mongo`

# Namespaces

| Name            | Description                                                                                                           |
| --------------- | --------------------------------------------------------------------------------------------------------------------- |
| default         | the resources you create locates here using 'kubectl create namespaces <name_of_namespace>' or with config (yaml)file |
| kube-node-lease | maintain the information of each node with lease object (heart beat of node)                                          |
| kube-public     | public available info, config map with cluster info which we get by `kubectl cluster-info`                            |
| kube-system     | contains system, master, kubctl process (DO NOT MODIFY)                                                               |

#### configMap and secretConfig limited to indiviual namespace cant share

#### services can be shared across namespaces

#### Vol & node are at cluster level cant be created in namespaces

#### If you dont pass namespace it will create in default namespace

#### If you want to avoid every time passing `-n <ns>` then use `kubens <ns_name` and `kubens` to see active ns. to install `brew install kubectx`

# Ingress

`minikube addons enable ingress` - to start k8s ingress controller
`kubectl get pods -n ingress-nginx` - to get the ingress controller pods. Note. check namespace if could not get it.
`kubectl get ingress` with this you able to see IP address
`vi /etc/hosts` add IP and DNS name

##### For below kind of error use `kubectl delete validatingwebhookconfigurations ingress-nginx-admission` command

```txt
rror from server (InternalError): error when creating "ingress.yaml": Internal error occurred:
failed calling webhook "validate.nginx.ingress.kubernetes.io": failed to call webhook:
Post "https://ingress-nginx-controller-admission.ingress-nginx.svc:443/networking/v1/ingresses?timeout=10s":
service "ingress-nginx-controller-admission" not found

```

# Example to access db from browser with mongodb and mongodb express pod running

| No. | Steps                                           | What to do?                                                                           |
| --- | ----------------------------------------------- | ------------------------------------------------------------------------------------- |
| 1   | create deployement and service file for mongodb |                                                                                       |
| 2   | create secret file to store credentials         | `echo -n 'username' \| base64` to encode the key and `kubectl apply -f <secret_file>` |
| 3   | create configMap file to properties             | 'kubectl apply -f <config_file_name>'                                                 |
| 4   | create mongo express deployment and service     | 'kubectl apply -f <file_name>'                                                        |
| 5   | start load balancer service                     | 'minikube service <service_name>' here it will be mongo express service               |

> [!IMPORTANT]
> it will show external ip as <pending> in case of minikube only
