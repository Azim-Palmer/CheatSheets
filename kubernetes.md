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
  **Troubleshooting**
  ```kubectl get``` : list resources\
  ```kubectl describe``` : show detailed information about a resource\
  ```kubectl logs``` : print the logs from a container in a pod\
  ```kubectl exec``` : execute a command on a container in a pod\
  ```kubectl exec -ti {PodName} bash``` : starts bash inside a pod\
  
  **network**\
  ```kubectl proxy``` : Expose the pods private network (without using ingress etc)\
  ```kubectl expose deployment/{DeploymentName} --type="NodePort" --port {port}```
  
