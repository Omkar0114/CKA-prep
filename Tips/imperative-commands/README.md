# Imperative commands to create and manage k8s objects
### works fast to save time

- create a pod with label -
`kubectl run redis -l tier=db --image=redis:alpine`

- Create a service redis-service to expose the redis application within the cluster on port 6379
`k expose pod redis --port=6379 --name redis-service`

- create a deployment with 3 replicas - `kubectl create deployment webapp --image=image-name --replicas=3`

- create a pod and expose it on port 8080 - `k run podName --image=imageName --port=8080`

- create a new namespace dev-ns - `k create ns dev-ns`

- create deployment in dev-ns, replicas=3, image=redis - `kubectl create deployment redis-deploy --image=redis --replicas=2 -n dev-ns`

- Create a pod called httpd using the image httpd:alpine in the default namespace. Next, create a service of type ClusterIP by the same name (httpd). The target port for the service should be 80 - `kubectl run httpd --image=httpd:alpine --port=80 --expose`
