# Scheduler is the k8s component which is responsible for scheduling pods across kubernetes cluster

- If pod status is pending, check the default k8s objects in the kube-system namespace whether the scheduler is present or not -  
`k get pods -n kube-system`

- Manually scheduling pods - 
In the defination.yaml file add the one more property `nodeName: ` under the spec section and specify name of your node.
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx 
spec:
  nodeName: node01
  containers:
    - image: nginx
      name: nginx-container
  
```

- If you want to replace a pod or recreate it but its already running, instead of deleteing and creating pod again, do it with one command - 
`k replace --force -f nginx.yaml`

- If container status is containerCreating add --watch flag to watch on status of pod - `k get pods --watch`
