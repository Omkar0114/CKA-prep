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
