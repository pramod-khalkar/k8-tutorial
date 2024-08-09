# How to run mongo setup

### Setup deployment and service

- `kubectl apply -f` [secret map](./mongo-secret.yaml) `echo -n 'username' \| base64` to encode the key
- `kubectl apply -f` [config map](./mongo-configmap.yaml)
- `kubectl apply -f` [mongodb deployment & service](./mongodb-deployment.yaml)
- `kubectl apply -f` [mongo express deployement & service](./mongo-express-deployment.yaml)
- `minikube service <service_name>` start service & test in browser
  > [!NOTE] Uncomment NodePort and LoadBalancer

### How to access portal/app through ingress locally

- `minikube addons enable ingress` to start k8s ingress controller
- `minikube addons enable ingress-dns` enable ingress-dns
- `kubectl get pods -n ingress-nginx` - to get the ingress controller pods running. Note. check namespace if could not get it.
- `kubectl get ingress` with this you able to see IP address
- `vi /etc/hosts` add IP and DNS mapping `127.0.0.1 app.com.example`
  > [!NOTE] DONT USE MINIKUBE IP
- `minikube tunnel` keep it running
- `app.com.example` hit in browser you should see page now...

> [!IMPORTANT]
> it will show external ip as <pending> in case of minikube only
