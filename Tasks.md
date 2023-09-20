### 
### 
 


### Problem 1 Create Pods in Kubernetes Cluster

  
```
apiVersion: v1
kind: Pod
metadata:
    name: pod-nginx
    labels:
      app: nginx_app
spec:
    containers:
    - name: nginx-container
      image: nginx:latest
```

## Create Deployments in Kubernetes Cluster
```
kubectl get deploy
kubectl get namespace
kubectl create deploy nginx --image nginx:latest
```

### Create Namespaces in Kubernetes Cluster


### Set Limits for Resources in Kubernetes
Problem 4: Create a pod named httpd-pod and a container under it named as httpd-container, use httpd image with latest tag only and remember to mention tag i.e httpd:latest and 
set the following limits:
Requests: Memory: 15Mi, CPU: 100m
Limits: Memory: 20Mi, CPU: 100m

```
apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod
spec:
  containers:
  - name: httpd-container
    image: httpd:latest
    resources:
      requests:
        memory: "15Mi"
        cpu: "100m"
      limits:
        memory: "20Mi"
        cpu: "100m"

```

### Rolling Updates in Kubernetes 

Perform a rolling update for this application and incorporate nginx:1.18 image. The deployment name is nginx-deployment
Make sure all pods are up and running after the update.

``` 
k describe deployment
kubectl set image deployment/nginx-deployment nginx-container=nginx:1.18
```

 
### Rollback a Deployment in Kubernetes

### Create Replicaset in Kubernetes Cluster

### Create Cronjobs in Kubernetes
  
### Countdown job in Kubernetes
 
### Kubernetes Time Check Pod
 
### Troubleshoot Issue With Pods
 
### Update an Existing Deployment in Kubernetes
 
### ReplicationController in Kubernetes
 
### Fix Issue with VolumeMounts in Kubernetes
