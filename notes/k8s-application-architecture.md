## Notes on deployment architecture in a k8s cluster

**Nodes** are/can be physical machines, or abstraction to a physical machine like VM.

**Pods** are an abstraction unit over containers. Generally a pod has one/many containers, but try to keep it as less in number as possible. This the unit which autoscales, so the smaller it is, the better.

**Ingress/LoadBalancer** is used to expose our application to outside.

**Persistent Volume** is used to persist data across 'auto-scaling'.