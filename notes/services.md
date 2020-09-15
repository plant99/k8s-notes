## Notes on services

### ClusterIP

`ClusterIP`, a type of `Service` can be used to expose ports within the cluster, it's the default k8s Service.

`kubectl` proxy allows admin to access services defined within ClusterIP, start a proxy with the following command

```sh
$ kubectl proxy --port=8080
```

One can access a specifi service by going to

http://localhost:8080/api/v1/proxy/namespaces/${NAMESPACE}>/services/${SERVICE-NAME}>:${PORT-NAME}>/


