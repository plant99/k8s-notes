## Things on setting up monitoring in a k8s cluster

In 2016, CoreOS team came up with a concept called Kubernetes Operator. They initially released operators for Prometheus, and etcd.

If some services in your cluster are used very often, i.e the likes of prometheus, etcd, redis.  You can create a central registry of all those services and configuration for each services lies with the creator of a particular service.

### Prometheus operator

Easiest way to install prometheus operator in a minikube cluster as mentioned [here](https://github.com/helm/charts/issues/11310#issuecomment-465331176) is as follows for reference.

```
helm install --namespace monitoring stable/prometheus-operator \
--set kubelet.serviceMonitor.https=true \
--set prometheus.prometheusSpec.serviceMonitorSelectorNilUsesHelmValues=false
```

### Service Monitors

After installing operator, to monitor services you write, you can add `ServiceMonitors` for your services and prometheus operators tap these service monitors and scrape the metrics from your service.

An example is shown here.

```
kubectl apply -f - <<END
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: example-app
spec:
  replicas: 3
  template:
    metadata:
      labels:
        app: example-app
    spec:
      containers:
      - name: example-app
        image: fabxc/instrumented_app
        ports:
        - name: web
          containerPort: 8080
---
kind: Service
apiVersion: v1
metadata:
  name: example-app
  labels:
    app: example-app
spec:
  selector:
    app: example-app
  ports:
  - name: web
    port: 8080
---
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: example-app
spec:
  selector:
    matchLabels:
      app: example-app
  endpoints:
  - port: web
END

```

**TODO**: Make notes on how to insert 'rules' and 'jobs' with Service Monitors.