# Components

## Pod

The smallest running unit of K8s.  
It is an abstraction over container, which can contain one or more containers .This allows user to switch between different container type.  
Usually, only one application running per pod.

## Config Map - Secret

Config map contains configurations for application so that you don't have to build the whole image again to apply changes.

Secret likes config map but used to store credential data.

Data in config map or secret can be used as environment variables or properties file

## Volume

Since K8s does not manage data persistence, if a pod crash and get recreated, all of its data will be lost => volumes are used to attack the storage (can be local or external) with the pod, they also be used to shared data between pods.  

A volume can be a folder or a drive inside a the host or in a remote server.

Volume's lifecircle bind to pod's lifecircle, so if the pod is restarted, it will be also restarted. PersistentVolume is used for store data that outlast the pod's life. Their lifecircle bind to the cluster's lifecircle.

```yml
spec:
  containers:
  - image: <image-name>
    name: <container-name>
    volumeMounts:
    - mountPath: /path
      name: test-volume
  volumes: # create the pod volume
  - name: test-volume
```

![volume](./img/volume.jpg)

## Deployment - replicasSet

Deployment and statefulSet are blue-print for creating pods so you could create multiple pods of an application to prevent down time.

Deployment would manage the replicasSet which then manage the pods (e.g scaling). You should edit the deployment only instead of replicasSet or pods. If you delete the deployment, the replicasSet and pods under it is also deleted.

## StatefulSet

StatefulSets are used for stateful application like databases. However, managing stateful application is somewhat tricky so they are usually kept outside of K8s.

## DeamonSet

DeamonSet just like deployment but ensures that all nodes run a copy of a pre-defined pod.

=> As nodes are added to the cluster, pods are added. As nodes are removed from the cluster, pods are garbaged collected.

It is usually used for: 

- logging
- node monitoring

## Service

Each pod will be assigned a IP address, which allow them to communicate with each other. Every time a pod is recreated, a new private IP address is assigned.

Service is a static IP address that can be attacked to each Pod. Since service's life circle and Pod's life circle are not connected, it allows to create a consistent communication chanel.

There are 4 type of service:

- ClusterId (default)  
  Create the virtual, internal address which can only be accessed within the cluster. The exposed port is the same with the application's port.
- NodePort  
  Create the ClusterId and also allocate high port on the node (to prevent conflix). Anyone can be access it via the high port if they have access to the host.
- ExternalName  
  Used for controlling the external services's name when the pods need to connect to external services. It works by creating CNAME DNS in the CoreDNS.
- LoadBalancer  
  Create the NodePorts along with a load balancer - this can behave differently depends on the kubernetes providers.

![deployment-statefulSet](./img/deployment-statefulSet.jpg)

## Ingress

When expose the application to outside world with a secure protocol and a domain name, the request will go to ingress and it will be forwarded to the service.(You could expose the application by external service but you have to access it via `http:node-address:service-port`)

![pod-service-ingress](./img/pod-service-ingress.jpg)