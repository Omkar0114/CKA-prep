# Monitoring Solution for Kubernetes

- k8s does not have the inbuilt monitoring solution. There are many open-source tools such as Prometheus, Datadog, etc. for monitoring metrics for the k8s cluster and its components.

## Kubernetes metrics server
- k8s have the metrics server which monitors the k8s cluster resources and saves logs to the in-memory database of the metrics server. It does not keep logs on the system.
- Apart from minikube for other tools we need to download the k8s metrics server from github and apply it to the k8s cluster.
``` bash 
>>> https://github.com/kubernetes-sigs/metrics-server

>>> k apply -f . 
```
## Checking logs with the metrics server
- `k top nodes` - to get node metrics/logs
- `k top pods` - to get pod logs
- `k top nodes --sort-by='cpu' --no-headers | head -1` - logs sorted by cpu & head -1 is for only get 1st resource which highly used CPU
- `k top pods --sort-by='memory' --no-headers | head -1` - get logs of pods sorted by memory

## Inspect the logs of kubernetes components
- `k logs <podname>` - to get logs of a specific pod
- `k logs <podname>  <containername>` - If you have multiple containers in the k8s pod you can specify the -c flag or container name to get logs.
