**minikube**\
 ```minikube start```\
 ```minikube delete``` : Completely delete the local minikube, a minikube start command will restart it\
 ```minikube dashboard``` : Installs and starts the Kubernetes control dashboard

**kubectl**\
 **Information**\
  ```kubectl cluster-info```\
  ```kubectl get {resourceType}```\
  ```kubectl api-resources``` : List all types of kubernetes resources (ex can be used to see what you can ```kubectl get {resourceType}```\
  ```kubectl logs {podname}```\
  ```kubectl version```\
  **deployment**\
  ```kubectl create deployment {deployment} --image={imageSource}```
  ```kubectl apply -f {filename}``` : Applies a particular file
  **Troubleshooting**
  ```kubectl get``` : list resources\
  ```kubectl describe``` : show detailed information about a resource\
  ```kubectl logs``` : print the logs from a container in a pod\
  ```kubectl exec``` : execute a command on a container in a pod\
  ```kubectl exec -ti {PodName} bash``` : starts bash inside a pod\
  **Config**\
  ```kubectl config get-contexts``` : # display list of contexts\
  ```kubectl config current-context``` : # display the current-context\
  ```kubectl config use-context {ClusterName}``` : sets kubectl's current context (useful when you have a local and remote cluster)\
  **network**\
  ```kubectl proxy``` : Expose the pods private network (without using ingress etc)\
    This means you can access it via http://localhost:8001/api/v1/namespaces/default/pods/{podName}/proxy/ - I don't know how it mpas different ports via the proxy yet\
  ```kubectl expose deployment/{DeploymentName} --type="NodePort" --port {port}```\
  ```minikube service {ServiceName} --url``` : **Required on Windows** Starts a service with a configured nodeport on Windows - YOU WONT BE ABLE TO ACCESS IT WITHOUT THIS ON WINDOWS\
  ```kubectl port-forward service/{serviceName} {port}```


**FAQ**\
**How do I expose a service running on localhost to a node?**
ssh into minikube (you might need to open Hyper-V manager and launch it with username root) run ```ping host.minikube.internal``` and use the ip it's using there\
**How do I access a service locally?**
 run ```minikube ip``` and navigate to that ip plus the nodePort specified in the service
 **How do I have Kubernetes use my local hard drive when I want to persist stuff?**
 1. First declare the mapping in Minikube - run as admin ```minikube mount {hostPath}:{nodeMountPath}``` e.g ```minikube mount C:\temp\minikube:/mnt/test```
 2. Create a PersistentVolume mapping to that 
 ```
 apiVersion: v1
kind: PersistentVolume
metadata:
  name: example-pv
spec:
  capacity:
    storage: 100Gi
  volumeMode: Filesystem
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Delete
  storageClassName: local-storage
  local:
    path: /mnt/test
  nodeAffinity:
    required:
      nodeSelectorTerms:
      - matchExpressions:
        - key: localTest
          operator: In
          values:
          - "yes"
```

3. - Create the associated claim
```apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: task-pv-claim
spec:
  storageClassName: local-storage
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 3Gi
```
      
4. Finally reference it in the container as a volume and volumeMount, use mountPath to direct where on the node the storage should be located
```  volumeMounts:
       - mountPath: "/var/lib/grafana"
         name : task-pv-claim
      volumes:
        - name: task-pv-claim
          persistentVolumeClaim:
            claimName: task-pv-claim
```
  
**Dashboard**
```kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')```
To generate a token
