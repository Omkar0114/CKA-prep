# CKA

### useful commands:

- `kubectl get pods`

- `kubectl get nodes`

- `kubectl get all -o wide` - to get all info about cluster objects and resources

- `kubectl desccribe pod pod-name` 

![image](https://github.com/Omkar0114/CKA-prep/assets/88308267/0b3c7532-f5b6-4118-8b26-f69a34a62eb1)

- The column READY shows that `running-containers-in-pod/total-containers-in-pod`

- `kubectl delete pod pod-name`

- We use kubectl run command with --dry-run=client -o yaml option to create a manifest file -
 
 `kubectl run redis --image=redis123 --dry-run=client -o yaml > redis-definition.yaml`
 
 - `kubectl create -f redis-definition.yaml`

# rs - replica-sets

- kubectl get rs 

- kubectl describe rs rs-name

- rs-defination.yaml file- 
 
![image](https://github.com/Omkar0114/CKA-prep/assets/88308267/27c71a3f-dd22-4c1e-a2ad-9212f4f8d3db)

- In the above image on the line 9 and 13 the `tier` label should be same with value `nginx`


- `k edit rs rs-name` - to edit rs resource

- `kubectl scale rs new-replica-set --replicas=5` - to scale rs to 5 pods

