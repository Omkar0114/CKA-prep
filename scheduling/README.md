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


# Node Selectors and node Affinity
- condition - If there are multiple nodes of different configuration and resource limits such as in size large or small and also we have different kind of Pods also have different size w.r.t. specifications then we make sure that large pods should run on the Large nodes. That's why we have node selectors and node affinity. 
- Node selectors are for the labeling the nodes with the value with key-pair value.
- `kubectl label --help ` - you get all info about label command 
### e.g- Apply a label on a node name node01
- `kubeclt label node node01 color=blue` - color=blue is the label 
- `kubectl get nodes --show-labels` - to show all labels on all nodes

Now we applied a label on node. now we have to design apod-defination.yaml file to assign such pods to perticular nodes.

- there is a property call affinity- nodeaffinity.

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: color
            operator: In
            values:
            - blue            
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
```

