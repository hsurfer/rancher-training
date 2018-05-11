## Containers platform 
- Intro and presentation 
- Rancher platform
- Practices

---

###  Intro and presentation

- Microservices architecture requires new infrastructure components. 
- Massive dynamism, portability and extensibility are required. 
- Current cloud platforms are not portable neither extensible.


---

Principal components
- Scheduler/orchestrator: How and where you container will be deployed.
- Network: Network layer to communicate containers between them avoiding port conflict. 
- Storage: Storage service to be able to share and persist the services data.
- Service discovery: Information about what and where services are running in the system.
- Service management: Manage access to the services in a HA and load balance scenarios.

---

####  Scheduler/orchestrator

A container scheduler is a piece of software that manages the server resources and deployment into them. It knows all the servers that provide resources (cpu and memory), how much they offer and how much resource are free. Based on the work load of every server, the scheduler will deploy the containers in the most free server, in order to manage the global load of the system.

Also, the scheduler is responsible to move or to rebalance the services if a server enter in maintenance mode or goes down, and to assure that the services are running in the scale that you define for them.

---

Principal scheduler/orchestrator in the market

<img src="slides/Containers_Platform/slides/images/scheduler.jpg", style="height:600; width:auto; background-color:white; float:center;"/>
 

---

#### Network

Network overlay is a service that provide the communication between containers independent from the hosts. It would generate a flat overlay network that provide an ip to every single container wide all hosts.

It helps to avoid networking collision and/or overlap between all the services exposing services in your system. 

---

Principal network services in the market

<img src="slides/Containers_Platform/slides/images/network.jpg", style="height:auto; width:900; background-color:white; float:center;"/>

---

####  Storage

Storage service makes the tasks to manage and provide persintence to your services. It's specially important in statefull and/or db services that has to persist and share data.

Basically, you could choose between block storage, fs storage or object storage. 

---

Principal storage services in the market

<img src="slides/Containers_Platform/slides/images/storage.jpg", style="height:auto; width:900; background-color:white; float:center;"/>

---

#### Service discovery

A system discovery is a distributed key/value service that knows all the information about our services. When you add a new service, it will be added to the system discovery, when you scale an already deployed service a new backend will be added or removed to the system discovery. 

Users or services could talk with service discovery in order to know how to communicate with a service, for examples which are the backends of a services??

System discovery is dependent of the scheduler you are using.

---

Principal Service discovery in the market

<img src="slides/Containers_Platform/slides/images/service_discovery.jpg", style="height:600; width:auto; background-color:white; float:center;"/>

---

#### Service management

A service management is a platform service that provides access to the services, providing a load balancing and high availability features. 

The service management provides an indirection layer to access the services. It could manages a service with dynamic backends that provide it or the access to different versions of the service. 

Load balancer could be external or internal, depending the use of them.


---

Principal service management in the market

<img src="slides/Containers_Platform/slides/images/service_management.jpg", style="height:auto; width:900; background-color:white; float:center;"/>

---

#### Container Platform

<img src="slides/Containers_Platform/slides/images/container_platform.jpg", style="height:600; width:auto; background-color:white; float:center;"/>

---

Functionality is the most important...
<img src="https://raw.githubusercontent.com/cncf/landscape/master/landscape/CloudNativeLandscape_latest.png", style="height:600; width:auto; background-color:white; float:center;"/>

---

### Rancher platform

- Rancher is an opensource containers platform, designed to be open and avoid vendor locks. 
- It provides a unified platform from hosts to microservices. 
- It's a multi environment platform.
- It provides and manages principal market scheduler/orchestrator.
- It provides a full API and CLI to automate and integrate with other pieces. 
- It provides some useful services as user auth, registry management, ssl certs management...
- It could be run in a local vm or in a few cloud machines.

---

#### Overview

<img src="slides/Containers_Platform/slides/images/rancher-overview.jpg", style="height:auto; width:900; background-color:white; float:center;"/>

---

#### Platform Schema
Manage multiple isolated environments
<img src="slides/Containers_Platform/slides/images/platform.jpg", style="height:auto; width:900; background-color:white; float:center;"/>

---

#### Environment
Environments by functionality
<img src="slides/Containers_Platform/slides/images/rancher-environment.jpg", style="height:auto; width:900; background-color:white; float:center;"/>

---

#### Lifecycle environments
DEV (Local vm)

<img src="slides/Containers_Platform/slides/images/rancher-diagram.png", style="height:auto; width:900; background-color:white; float:center;"/>

---

PRO HA + Multicloud machines

<img src="slides/Containers_Platform/slides/images/rancher-HA-diagram.png", style="height:auto; width:900; background-color:white; float:center;"/>

---

#### Hosts
Provide host from multiple cloud providers 
<img src="slides/Containers_Platform/slides/images/rancher-host.jpg", style="height:auto; width:900; background-color:white; float:center;"/>

---

#### Schedulers
Choose orchetrator by environment
<img src="slides/Containers_Platform/slides/images/rancher-schedulers.jpg", style="height:auto; width:900; background-color:white; float:center;"/>

---

#### Network
Choose the network management
<img src="slides/Containers_Platform/slides/images/rancher-network.jpg", style="height:auto; width:900; background-color:white; float:center;"/>

---

#### Storage
Choose storage backend
<img src="slides/Containers_Platform/slides/images/rancher-storage.jpg", style="height:auto; width:900; background-color:white; float:center;"/>

---

#### Service Discovery
Built in service discovery
<img src="slides/Containers_Platform/slides/images/rancher-SDiscovery.jpg", style="height:auto; width:900; background-color:white; float:center;"/>

---

#### Service Management
HAproxy, traefik or external load balancers
<img src="slides/Containers_Platform/slides/images/rancher-SManagement.jpg", style="height:auto; width:900; background-color:white; float:center;"/>

---

#### Catalog
One click deploy already integrated services
<img src="slides/Containers_Platform/slides/images/rancher-catalog.jpg", style="height:550; width:auto; background-color:white; float:center;"/>

---

#### API
Full featured API 
<img src="slides/Containers_Platform/slides/images/rancher-api.jpg", style="height:auto; width:900; background-color:white; float:center;"/>

---

#### Overview

- Admin
- Infrastructure
- Environments
- Kubernetes
- API

---

#### Anatomy of a deployment

- A deployment could have one or many pods inside it. 
- Every deployment is independent in terms of run or scale.
- Definition by k8s yml files. 
- Every deployment could be accessed by others defining service. 
- Every deployment could be externally published defining ingress.
- Every service add a dns entry like <service>.<namespace>

---

### Example

Create deployments for every microservice defined in previuous examples and publish external access to it.

---

#### Deployments

Repositories and docker images:
- https://github.com/rawmind0/web-inventory - rawmind/web-inventory:0.1-0
- https://github.com/rawmind0/web-payments - rawmind/web-payments:0.1-3
- https://github.com/rawmind0/web-shipping - rawmind/web-shipping:0.1-0
- https://github.com/rawmind0/web-gateway - rawmind/web-gateway:0.1-3

---

shipping-deployment.yml
```
kind: Deployment
apiVersion: extensions/v1beta1
metadata:
  name: shipping
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: shipping
    spec:
      containers:
      - image: rawmind/web-shipping:0.1-0
        name: shipping
        ports:
        - containerPort: 8080
          protocol: TCP
```

---

payments-deployment.yml
```
kind: Deployment
apiVersion: extensions/v1beta1
metadata:
  name: payments
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: payments
    spec:
      containers:
      - image: rawmind/web-payments:0.1-3
        name: payments
        ports:
        - containerPort: 8080
          protocol: TCP
```

---

inventory-deployment.yml
```
kind: Deployment
apiVersion: extensions/v1beta1
metadata:
  name: inventory
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: inventory
    spec:
      containers:
      - image: rawmind/web-inventory:0.1-0
        name: inventory
        ports:
        - containerPort: 8080
          protocol: TCP
```

---

gateway-deployment.yml
```
kind: Deployment
apiVersion: extensions/v1beta1
metadata:
  name: gateway
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: gateway
    spec:
      containers:
      - image: rawmind/web-gateway:0.1-3
        name: gateway
        ports:
        - containerPort: 8080
          protocol: TCP
```

---

#### Services

---

shipping-service.yml
```
apiVersion: v1
kind: Service
metadata:
  name: shipping
  labels:
    app: shipping
spec:
  ports:
  - port: 8080
    targetPort: 8080
    protocol: TCP
    name: http
  selector:
    app: shipping
```
---

payments-service.yml
```
apiVersion: v1
kind: Service
metadata:
  name: payments
  labels:
    app: payments
spec:
  ports:
  - port: 8080
    targetPort: 8080
    protocol: TCP
    name: http
  selector:
    app: payments
```

---

inventory-service.yml
```
apiVersion: v1
kind: Service
metadata:
  name: inventory
  labels:
    app: inventory
spec:
  ports:
  - port: 8080
    targetPort: 8080
    protocol: TCP
    name: http
  selector:
    app: inventory
```

---

gateway-service.yml
```
apiVersion: v1
kind: Service
metadata:
  name: gateway
  labels:
    app: gateway
spec:
  ports:
  - port: 8080
    targetPort: 8080
    protocol: TCP
    name: http
  selector:
    app: gateway
```

---

#### Ingress

---

gateway-ingress.yml
```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: gateway-http
spec:
  rules:
  - http:
      paths:
      - backend:
          serviceName: gateway
          servicePort: 8080
```

---

#### Kubectl

```
kubectl create -f deployment_file   # Create on k8s every deployment

kubectl create -f service_file      # Create on k8s every service

kubectl create -f ingress_file      # Create on k8s every ingress
```

---

### Practices

---

#### Practice 1

Get the app dockers created in the previous stages, deploy an stack/services into the platform and access them.

---

### Practice 2

Make some change in one of the services and upgrade the already deployed stack/services.

---

### References

---

#### Web
- Cloud Native Landscape - https://github.com/cncf/landscape
- Rancher Site - http://rancher.com/
- Rancher Documentation - https://docs.rancher.com/rancher/v1.4/en/
- Try Rancher - https://try.rancher.com
- Hidden dependencies - http://rancher.com/hidden-dependencies-with-microservices/

---

#### Training & videos
- Rancher free monthly training sessions - https://attendee.gotowebinar.com/rt/2905734731496917249
- Rancher youtube channel - https://www.youtube.com/channel/UCh5Xtp82q8wjijP8npkVTBA


