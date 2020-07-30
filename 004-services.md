## Introducing services
* A Kubernetes Service is a resource you create to make a single, constant point of entry to a group of pods providing the same service.
* Each service has an IP address and port that never change while the service exists.
* Clients can open connections to that IP and port, and those connections are then routed to one of the pods backing that service.
* This way, clients of a service don’t need to know the location of individual pods providing the service, allowing those pods to be moved around the cluster
at any time.
* 

## Connecting to services living outside the cluster
* Up to now, we’ve talked about services backed by one or more pods running inside the cluster.
* But cases exist when you’d like to expose external services through the Kubernetes services feature.
* Instead of having the service redirect connections to pods in the cluster, you want it to redirect to external IP(s) and port(s).
* This allows you to take advantage of both service load balancing and service discovery.
* Client pods running in the cluster can connect to the external service like they connect to internal services.
* 



## Exposing services to external clients
* Up to now, we’ve only talked about how services can be consumed by pods from inside the cluster
* But you’ll also want to expose certain services, such as frontend webservers, to the outside, so external clients can access them.
* You have a few ways to make a service accessible externally:
   * Setting the service type to NodePort —For a NodePort service, each cluster node opens a port on the node itself (hence the name) and redirects traffic
   received on that port to the underlying service. The service isn’t accessible only at the internal cluster IP and port, but also through a dedicated port o
   all nodes.
   * Setting the service type to LoadBalancer , an extension of the NodePort type—This makes the service accessible through a dedicated load balancer, provisioned
   from the cloud infrastructure Kubernetes is running on. The load balancer redi- rects traffic to the node port across all the nodes. Clients connect to the 
   service through the load balancer’s IP.
   * Creating an Ingress resource, a radically different mechanism for exposing multiple services through a single IP address—It operates at the HTTP level 
   (network layer 7) and can thus offer more features than layer 4 services can.






Exposing services externally through an Ingress resource
Signaling when a pod is ready to accept connections
Using a headless service for discovering individual pods
Troubleshooting services
Summary
