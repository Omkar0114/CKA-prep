Q1 - Print the names of all deployments in the admin2406 namespace in the following format:
  DEPLOYMENT CONTAINER_IMAGE READY_REPLICAS NAMESPACE
  <deployment name> <container image used> <ready replica count> <Namespace>
  The data should be sorted by the increasing order of the deployment name.

  Example:

  DEPLOYMENT CONTAINER_IMAGE READY_REPLICAS NAMESPACE
  deploy0 nginx:alpine 1 admin2406
  Write the result to the file /opt/admin2406_data.

Ans - 
    kubectl -n admin2406 get deployment -o custom columns=DEPLOYMENT:.metadata.name,CONTAINER_IMAGE:.spec.template.spec.containers[].image,READY_REPLICAS:.status.readyReplicas,NAMESPACE:.metadata.namespace --sort-by=.metadata.name > /opt/admin2406_data

---- 

Q2 - Create a pod called secret-1401 in the admin1401 namespace using the busybox image. The container within the pod should be called secret-admin and should sleep for 4800 seconds.

The container should mount a read-only secret volume called secret-volume at the path /etc/secret-volume. The secret being mounted has already been created for you and is called dotfile-secret.

ans - Use the command kubectl run to create a pod definition file. Add secret volume and update container name in it.

Alternatively, run the following command:

`kubectl run secret-1401 -n admin1401 --image=busybox --dry-run=client -oyaml --command -- sleep 4800 > admin.yaml`
Add the secret volume and mount path to create a pod called secret-1401 in the admin1401 namespace as follows:
```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: secret-1401
  name: secret-1401
  namespace: admin1401
spec:
  volumes:
  - name: secret-volume
    # secret volume
    secret:
      secretName: dotfile-secret
  containers:
  - command:
    - sleep
    - "4800"
    image: busybox
    name: secret-admin
    # volumes' mount path
    volumeMounts:
    - name: secret-volume
      readOnly: true
      mountPath: "/etc/secret-volume"
```
