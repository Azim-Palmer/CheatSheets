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
  **Config**\
  ```kubectl config get-contexts``` : # display list of contexts\
  ```kubectl config current-context``` : # display the current-context\
  ```kubectl config use-context {ClusterName} : sets kubectl's current context (useful when you have a local and remote cluster)\
  
  **network**\
  ```kubectl proxy``` : Expose the pods private network (without using ingress etc)\
    This means you can access it via http://localhost:8001/api/v1/namespaces/default/pods/{podName}/proxy/ - I don't know how it mpas different ports via the proxy yet\
  ```kubectl expose deployment/{DeploymentName} --type="NodePort" --port {port}```\
  ```minikube service {ServiceName} --url``` : **Required on Windows** Starts a service with a configured nodeport on Windows - YOU WONT BE ABLE TO ACCESS IT WITHOUT THIS ON WINDOWS\
  
