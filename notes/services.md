## Notes on services

### ClusterIP

`ClusterIP`, a type of `Service` can be used to expose ports within the cluster, it's the default k8s Service.

`kubectl` proxy allows admin to access services defined within ClusterIP, start a proxy with the following command

```sh
$ kubectl proxy --port=8080
```

One can access a specific service by going to

http://localhost:8080/api/v1/proxy/namespaces/${NAMESPACE}>/services/${SERVICE-NAME}>:${PORT-NAME}>/


### NodePort

This service allows you to bind machine's port to service's host, port. A limitation of NodePort is you can define only one NodePort per service.

### LoadBalancer

LoadBalancer services are used very commonly in production, and it distributes requests across a range of pods defined by 'replicas'.

Doesn't work with minikube.

### Ingress

Not a service, kind of a smart-router. Nginx for k8s deployments.