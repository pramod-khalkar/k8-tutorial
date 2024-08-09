Problem:

```txt
rror from server (InternalError): error when creating "ingress.yaml": Internal error occurred:
failed calling webhook "validate.nginx.ingress.kubernetes.io": failed to call webhook:
Post "https://ingress-nginx-controller-admission.ingress-nginx.svc:443/networking/v1/ingresses?timeout=10s":
service "ingress-nginx-controller-admission" not found

```

Solution :

`kubectl delete validatingwebhookconfigurations ingress-nginx-admission` command
