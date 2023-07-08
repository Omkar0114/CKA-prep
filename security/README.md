# Kubeconfig file
- kubeconfig file is default located at `~/root/.kube/config` and saves all information about the cluster.
- kubeconfig file mainly saves 3 components about cluster -
  1. Clusters
  2. Contexts
  3. Users
  And combine with each other when dealing with `kube-api-server

# Commands 
- `kubectl config -h` - to view all commands
-  `k config view` - to see all cluster information
-  `k config use-context context_name` - to use particular k8s context
-  `k config --kubeconfig=/root/my-kube-config use-context context name` -  --kubeconfig flag loads the config file if you have another one, otherwise, it talks with the `~/root/.kube/config` file by default 

# Authorization 
- K8s docs - https://kubernetes.io/docs/reference/access-authn-authz/authorization/

- There are various modes of authorization in kubernetes. Which allows us or resources to talk with the kube-api server.
- `k describe pod kube-apiserver-controlplane -n kube-system | grep -i auth` - to check authorization modes in the cluster
- `k get roles` - to check roles in the default namespace
- `k get roles -A --no-headers | wc -l` - -A for all namespace, wc -l for counting lines & --no-headers for not counting header line
- `k describe role rolename -n namespace` - to describe and view the resources access given to

### Roles and Rolebinding
- roles are the specific user groups to the k8s can give permission and rolebinding is the binding the user to that specific role to acces k8s resources
- `k get roles` - to get roles
- `kubectl describe rolebinding kube-proxy -n kube-system` - to describe info about kube-proxy role in KS namespace

- To create role and rolebinding -
- `k create role -h`
- `k create rolebinding -h`
- ex - `kubectl create role developer --namespace=default --verb=list,create,delete --resource=pods`
- ex - `kubectl create rolebinding dev-user-binding --namespace=default --role=developer --user=dev-user`

- Also you can make a YAML file to create via declarative approach
```
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  namespace: default
  name: developer
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["list", "create","delete"]

---
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: dev-user-binding
subjects:
- kind: User
  name: dev-user
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: developer
  apiGroup: rbac.authorization.k8s.io
```

- `k edit role rolename -n namespace` -  to edit a specific role and add some permissions
- `k edit rolebinding ` - to edit rolebinding

### Similar there are Clusterroles & ClusterRolebindings which are for cluster scoped
