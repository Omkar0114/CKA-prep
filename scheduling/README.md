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


# Selectors & labels 

- There are multiple pods with multiple lables and selectors. We can identify them using `--selector ` flag and extract it and find it easily.

- If you want to find pods in the dev enviroment Use - `k get pods --selector env=dev` command

- above command outputs the no of lines are there. _TIP_ - get number of pods/any-resource with only one command - `k get pods --no-headers | wc -l`
*`--no-headers` is for not counting 1st header line of list of pods & `wc -l` is the counting no. of lines*

- Make sure you have same labels in yaml file in the _spec_ & _template_ section - 

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx 
spec:
  nodeName: node01
  selector:
    matchlabels:
      tier: front-end
  containers:
    - image: nginx
      name: nginx-container
  template:
    metadata:
      labels:
        tier: front-end
  
```

# Taints & Tolerations
- Taints are set on _nodes_ and tolerations are set on _pods_
