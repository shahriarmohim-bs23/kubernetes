
# Poridhi lab-service
  By using a simple rest API, users can launch their own virtual machines over SSH or open the lab terminal in a web browser.
  

## Overview

Poridhi lab-service running in a kubernetes cluster.There is a master node and two worker node in the cluster.They are in the same subnet.
poridhi-lab-controller service is responsible for lab instance deployment.
It can communicate with cluster's api.Inside the poridhi-lab-controller
pod a flask app running.Flask app can communicate with kubernetes using kubernetes client.
It can luanch namespace,service,deployment,ingressroute.
poridhi-lab-controller is the admin  in the Role base authentication.
Whenever i request for a lab in poridhi-lab-controller kubernetes
client will create lab instance in the kubernetes cluster 
with an unique name.
![App Screenshot](https://github.com/shahriarnasif/kubernetes/blob/main/Untitled%20Diagram.drawio.png?raw=true)


## poridhi-lab-controller
 In every poridhi-lab-controller deployment in 
  default namespace there is an ingress,
  service and pod deployment.Ingressroute onboard the external 
  request and it's hostname is lab.poridhi.io.Ingress sends the 
  request
  to the service and service sends 
  the request to the pod.
  

 

 

## Lab-instance
Lab launch in different namespace.It generated unique name for namespce.
e.g:term-'xyz',term-'abc' etc.There also a pod,service and an ingressroute will be created.
Ingress dns will be e.g:term-xyz.poridhi.io..A background task will terminate lab instance after one hour.
![App Screenshot](https://github.com/shahriarnasif/kubernetes/blob/main/Untitled%20Diagram.drawio(2).png?raw=true)



## New Lab-instance
In our upcoming lab  xterm,postgres,redis instance will be created in same namespace.
In xterm instance there will have a pod,service and ingress.
But in redis and postgress only pod and service will be created.
A dns name will be attached in ingressroute.As instances are in same namespace so we can access
redis and postgres instance also.
![App Screenshot](https://github.com/shahriarnasif/kubernetes/blob/main/Untitled%20Diagram.drawio(4).png?raw=true)



