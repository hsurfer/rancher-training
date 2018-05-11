## K101 - Intro to Kubernetes - TU:1

---

### Synopsis

This is the introduction to kubernetes (k8s) concepts for those who have never encountered them. It is conceptual, laying the foundation for information delivered in later courses.

---

### Learning Objectives

At the end of this course, a student will understand 
- what k8s is. 
- how k8s architecture is. 
- how k8s operates.
- how to think about infrastructure that run within k8s.

---

### Prerequisites

None.

---

### Topics

- What is K8s?
- Architecture
- Deployment types
- Services
- References

---

### What is k8s?

K8s... 
- is a portable, extensible open-source platform for managing containerized workloads and services. 
- facilitates both declarative configuration and automation. 
- has a large, rapidly growing ecosystem. 
- services, support, and tools are widely available.

---

### Architecture

K8s has 3 distinct planes for its services:
- Etcd plane: etcd service that provides persistence to k8s cluster data.
- Control plane: k8s/Rancher stateless components which orchestrate and manage the Compute Plane.
- Worker plane: real workload (k8s pods), orchestrated and managed by control plane.

For production, running each plane runs on dedicated physical or virtual hosts is recommneded. For development, overlapping planes may be used to simplify management and reduce costs.

---

#### Architecture
<img src="slides/Kubernetes/slides/images/k8s-scheme-v2.0.jpg", style="width:auto; height:auto; background-color:white; align:center;"/>

---

#### Etcd Plane
Comprised of etcd cluster services which persist data ok k8s cluster. 

- etcd
- cattle-node-agent (if k8s cluster is managed by Rancher)

Resiliency is achieved by adding 3 hosts to this plane.

---

#### Etcd Plane
<img src="slides/Kubernetes/slides/images/data_plane-scheme.jpg", style="width:auto; height:auto; background-color:white; align:center;"/>

---

#### Control Plane
k8s/Rancher stateless and scalable components which orchestrate and manage worker plane:
- kube-apiserver
- kube-scheduler
- kube-controller-manager
- cattle-cluster-agent (if k8s cluster is managed by Rancher)
- cattle-node-agent (if k8s cluster is managed by Rancher)

---

#### Control Plane
<img src="slides/Kubernetes/slides/images/control_plane-scheme.jpg", style="width:auto; height:auto; background-color:white; align:center;"/>

---

#### Worker Plane
Comprised of the real workload (Kubernetes pods) and k8s/Rancher components, orchestrated and managed by k8s control plane:
- kubelet
- kube-proxy
- cattle-node-agent (if k8s cluster is managed by Rancher)

---

#### Worker Plane
<img src="slides/Kubernetes/slides/images/worker_plane-scheme.jpg", style="width:auto; height:auto; background-color:white; align:center;"/>

---

### Deployment Types

- Standalone: recommended for development and training. 
- Overlapping planes: recommended for ephemeral environments and training. 
- Separated planes: recommended for production.

---

#### Standalone

Characteristics
- Simple, low-cost environment for development and training
- No resiliency to host failure
- Low performance

Instructions
- Create 1 host with >=1 CPU and >=4GB RAM.
- Create RKE template with 3 roles at single node.
- Deploy RKE cluster.

---

#### Standalone
<img src="slides/Kubernetes/slides/images/standalone-scheme-v2.0.jpg", style="width:auto; height:auto; background-color:white; align:center;"/>

---

#### Overlapping planes

Characteristics
- Simple, low-cost environment for ephemeral and training
- Data plane and control plane resilient to minority of hosts failing
- Worker plane resiliency depends on the deployment plan
- Potential performance issues with etcd/k8s components

---

#### Overlapping planes

Instructions
- Create 3 hosts with >=1 CPU and >=4GB RAM.
- Create RKE template with 3 roles at every node.
- Deploy RKE cluster.

---

#### Overlapping planes
<img src="slides/Kubernetes/slides/images/overlapped_planes-scheme-v2.0.jpg", style="width:auto; height:auto; background-color:white; align:center;"/>

---

#### Separated planes

Characteristics
- Data plane resilient to minority of hosts failing.
- Control plane resilient to all but one host failing.
- Worker plane resiliency that is dependent on the deployment plan.
- High-performance, production-ready environment.

---

Instructions
- Create 7 hosts with >=1 CPU and >=4GB RAM.
- Create RKE template with 
  - 3 nodes with etcd role.
  - 2 nodes with controlplane role.
  - 2 nodes with worker role.
- Deploy RKE cluster.

---

#### Separated planes

<img src="slides/Kubernetes/slides/images/separated_planes-scheme-v2.0.jpg", style="width:auto; height:auto; background-color:white; align:center;"/>

---

### Services

Based on functionality, services are split into 4 categories:
- K8s master: k8s services that conform etcd and control planes.
- K8s node: k8s services that conform worker plane.
- K8s addons: k8s optional services that extend k8s functionality.
- Rancher services: rancher services at all planes to control and manage k8s cluster.

https://kubernetes.io/docs/concepts/overview/components/

---

#### K8s master

- etcd: Distributed key/value storage to provide cluster data persistence.
- kube-apiserver: K8s API, front-end for the Kubernetes control plane.
- kube-scheduler: Schedule new pods into k8s nodes. Scheduling decisions include individual and collective resource requirements, hardware/software/policy constraints, affinity and anti-affinity specifications, data locality, inter-workload interference and deadlines

---

#### K8s master

- kube-controller-manager: set of patform controllers:
  - Node Controller: noticy and responding when nodes go down.
  - Replication Controller: maintain the correct number of pods for every replication controller object in the system.
  - Endpoints Controller: Populates Endpoints object (that is, joins Services & Pods).
  - Service Account & Token Controllers: Create default accounts and API access tokens for new namespaces.

---

#### K8s master

- cloud-controller-manager: interacts with the underlying cloud providers. 

  cloud-controller-manager allows cloud vendors code and k8s core to evolve independent of each other. In prior releases, the core Kubernetes code was dependent upon cloud-provider-specific code for functionality. In future releases, code specific to cloud vendors should be maintained by the cloud vendor themselves, and linked to cloud-controller-manager while running k8s.

---

#### K8s master
The following controllers have cloud provider dependencies:

- Node Controller: determines if a node has been deleted in the cloud after it stops responding.
- Route Controller: setup routes in the underlying cloud infrastructure
- Service Controller: Creates, updates and deletes cloud provider load balancers
- Volume Controller: Creates, attachs, and mounts volumes to pods, interacting with the cloud provider.


---

#### K8s node

- kubelet: Agent that runs on each node in the cluster. It makes sure that containers are running in a pod.

  The kubelet takes a set of PodSpecs that are provided through various mechanisms and ensures that the containers described in those PodSpecs are running and healthy. The kubelet doesn’t manage containers which were not created by Kubernetes.

---

#### K8s node

- kube-proxy: K8s service abstraction by maintaining network rules on the host and performing connection forwarding to services.

- Container runtime: Software that is responsible for running containers. K8s supports several runtimes: Docker, rkt, runc and any OCI runtime-spec implementation.

---

#### K8s addons

Some typical addons: 
- DNS: K8s cluster dns to maintain  dns records for services. 
- Web UI: allows users to manage and troubleshoot applications running in the cluster. 
- Container Resource Monitoring: records generic time-series metrics about containers in a central database, and provides a UI for browsing that data.

---

#### Rancher services

These services would be running if k8s cluster is managed by Rancher:
- cattle-cluster-agent: Rancher Cluster agent that connect and report cluster status to rancher API.
- cattle-node-agent: Rancher node agent that connect and report node status to rancher API.

---

### References

---

#### Web
- K8s Official Documentation - https://kubernetes.io/docs/home/
- K8s components - https://kubernetes.io/docs/concepts/overview/components/
- K8s addons - https://kubernetes.io/docs/concepts/cluster-administration/addons/
  - https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/
  - https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
  - https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/

