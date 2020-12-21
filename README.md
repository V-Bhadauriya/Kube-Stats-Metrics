## Kube State Metrics
kube-state-metrics is a simple service that listens to the Kubernetes API server and generates metrics about the state of the objects. (See examples in the Metrics section below.) It is not focused on the health of the individual Kubernetes components, but rather on the health of the various objects inside, such as deployments, nodes and pods.
Get More Detail Here:
[kube-state-metrics](https://github.com/kubernetes/kube-state-metrics)


## Deployment
``git clone https://github.com/V-Bhadauriya/Kube-Stats-Metrics.git``
``kubectl apply -f Kube-Stats-Metrics/cluster-role.yaml``
``kubectl apply -f Kube-Stats-Metrics/cluster-role-binding.yaml``
``kubectl apply -f Kube-Stats-Metrics/service-account.yaml``
``kubectl apply -f Kube-Stats-Metrics/deployment.yaml``
``kubectl apply -f Kube-Stats-Metrics/cluster-role.yaml``
``kubectl apply -f Kube-Stats-Metrics/service.yaml``

## Prometheus config
Add the below job config in Prometheus Configuration configmap which your can find in **istio-system** namespace.

```
- job_name: 'k8s-kube-state-metrics-k8s-cluster'
  metrics_path: /metrics
  scheme: http
  static_configs:
    - targets: ['kube-state-metrics.kube-system.svc.cluster.local:8080']
  metric_relabel_configs:
    - target_label: cluster
      replacement: k8s-cluster
```

## Delete the Prometheus
Delete the Prometheus pod from the **istio-system** so that the updated config will be applied and Prometheus start scraping the the metrics.
**Command -:**
``
kubectl delete pod <PrometheusPodName> -n istio-system
``

After delete new pod will automatcially spins up.


## Grafana DashBoard
![alt text](https://raw.githubusercontent.com/V-Bhadauriya/Kube-Stats-Metrics/main/dashboard/screen-tex-light-th.png?raw=true)

