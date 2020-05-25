**minikube**\
 ```minikube start```\
 ```minikube delete``` : Completely delete the local minikube, a minikube start command will restart it\
 ```minikube dashboard``` : Installs and starts the Kubernetes control dashboard

**kubectl**\
 **Information**\
  ```kubectl cluster-info```\
  ```kubectl get nodes```\
  ```kubectl get deployments```\
  ```kubectl version```\
    
  **deployment**\
  ```kubectl create deployment {deployment} --image={imageSource}```
  
  **network**\
  ```kubectl proxy``` : Expose the pods private network (without using ingress etc)
  
