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
```
k rollout --help
kubectl rollout history deployment/nginx-deployment
kubectl rollout undo deployment/nginx-deployment --to-revision=1
```

### Create Replicaset in Kubernetes Cluster

Create a ReplicaSet using httpd image with latest tag only and remember to mention tag i.e httpd:latest and name it as httpd-replicaset.
Labels app should be httpd_app, labels type should be front-end.
The container should be named as httpd-container; also make sure replicas counts are 4.

```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: httpd-replicaset
spec:
  replicas: 4
  selector:
    matchLabels:
      app: httpd_app
      type: front-end
  template:
    metadata:
      labels:
        app: httpd_app
        type: front-end
    spec:
      containers:
      - name: httpd-container
        image: httpd:latest

```

### Create Cronjobs in Kubernetes
```
apiVersion: batch/v1
kind: CronJob
metadata:
  name: xfusion
spec:
  schedule: "*/3 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: cron-xfusion
            image: nginx:latest
            command:
            - /bin/sh
            - -c
            - echo Welcome to xfusioncorp!
          restartPolicy: OnFailure
k apply -f pod.yaml
k get cronjob
```
  
### Countdown job in Kubernetes

Create a job countdown-nautilus.The spec template should be named as countdown-nautilus (under metadata), and the container should be named as
container-countdown-nautilus
Use image debian with latest tag only and remember to mention tag i.e debian:latest, and restart policy should be Never.
Use command sleep 5
```
apiVersion: batch/v1
kind: Job
metadata:
  name: countdown-nautilus
spec:
  template:
    metadata:
      name: countdown-nautilus
    spec:
      containers:
      - name: container-countdown-nautilus
        image: debian:latest
        command:
        - sleep
        - "5"
      restartPolicy: Never

```


 
### Kubernetes Time Check Pod
Create a pod called time-check in the xfusion namespace. This pod should run a container called time-check, container should use the busybox image with latest tag only and remember to mention tag i.e busybox:latest.

Create a config map called time-config with the data TIME_FREQ=10 in the same namespace.

The time-check container should run the command: while true; do date; sleep $TIME_FREQ;done and should write the result to the location /opt/devops/time/time-check.log. Remember you will also need to add an environmental variable TIME_FREQ in the container, which should pick value from the config map TIME_FREQ key.

Create a volume log-volume and mount the same on /opt/devops/time within the container.


```
# Create the ConfigMap
kubectl create configmap time-config --namespace=xfusion --from-literal=TIME_FREQ=10
kubectl create ns xfusion

apiVersion: v1
kind: Pod
metadata:
  name: time-check
  namespace: xfusion
spec:
  containers:
  - name: time-check
    image: busybox:latest
    command:
    - sh
    - -c
    - while true; do date; sleep $TIME_FREQ; done >> /opt/devops/time/time-check.log
    env:
    - name: TIME_FREQ
      valueFrom:
        configMapKeyRef:
          name: time-config
          key: TIME_FREQ
    volumeMounts:
    - name: log-volume
      mountPath: /opt/devops/time
  volumes:
  - name: log-volume
    emptyDir: {}



```
 
### Troubleshoot Issue With Pods

There is a pod named webserver and the container under it is named as nginx-container. It is using image nginx:latest
There is a sidecar container as well named sidecar-container which is using ubuntu:latest image.
Look into the issue and fix it, make sure pod is in running state and you are able to access the app.
Note: The kubectl utility on jump_host has been configured to work with the
```
edit the spelling mistake latests to latest

```
 
### Update an Existing Deployment in Kubernetes
We already have a deployment named nginx-deployment and service named nginx-service. Some changes need to be made in this 
deployment and service, make sure not to delete the deployment and service.

1.) Change the service nodeport from 30008 to 32165
2.) Change the replicas count from 1 to 5
3.) Change the image from nginx:1.19 to nginx:latest
```
k edit svc
k edit deployment
kubectl edit svc nginx-service
kubectl scale deployment nginx-deployment --replicas=5
kubectl set image deployment/nginx-deployment nginx=nginx:latest

```
 
### ReplicationController in Kubernetes
Create a ReplicationController using httpd image, preferably with latest tag, and name it as httpd-replicationcontroller.
Labels app should be httpd_app, and labels type should be front-end. The container should be named as httpd-container and also make sure replica counts are 3.

```
apiVersion: v1
kind: ReplicationController
metadata:
  name: httpd-replicationcontroller
  labels:
    app: httpd_app
    type: front-end
spec:
  replicas: 3
  selector:
    app: httpd_app
    type: front-end
  template:
    metadata:
      labels:
        app: httpd_app
        type: front-end
    spec:
      containers:
      - name: httpd-container
        image: httpd:latest

```
 
### Fix Issue with VolumeMounts in Kubernetes

The pod name is nginx-phpfpm and configmap name is nginx-config. Figure out the issue and fix the same.
Once issue is fixed, copy /home/thor/index.php file from the jump host to the nginx-container under nginx document root and 
you should be able to access the website using Website button on top bar.

```
```
