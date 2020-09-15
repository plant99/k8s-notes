## Notes on deployment architecture in a k8s cluster

**Nodes** are/can be physical machines, or abstraction to a physical machine like VM.

**Pods** are an abstraction unit over containers. Generally a pod has one/many containers, but try to keep it as less in number as possible. This the unit which autoscales, so the smaller it is, the better.

**Ingress/LoadBalancer** is used to expose our application to outside.

**Persistent Volume** is used to persist data across 'auto-scaling'.

## Notes on k8s api

**kind** and **api** are related. To be more precise, there are many 'kinds' of configs under an 'api'.
E.g/ 'Pod' is under `api: v1` but 'Deployment' is under `api: apps/v1`

One can expose port with the help of `ports` and `containerPort` in the definition of a container.

For debugging kubectl can port-forward to your pod's exposed port in this way.

```sh
$ kubectl port-forward $PODNAME 3000:3000
```

[Services](https://medium.com/google-cloud/kubernetes-nodeport-vs-loadbalancer-vs-ingress-when-should-i-use-what-922f010849e0) are used to expose containers to external networks. Some types of services are NodePort, Ingress, LoadBalancer.

You can separate configs in the same file with a `---` on a new line. This won't be the case if you're using something like `skaffold` when the configs can be aggregrated within a directory.

Update [LoadBalancers doesn't work with `minikube`](https://stackoverflow.com/questions/44110876/kubernetes-service-external-ip-pending). One can still use Ingress, NodePort.
