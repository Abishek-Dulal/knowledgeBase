### Service discovery in the cloud 
service discovery agent in the cloud should be:-
1) **highly available**

2) **peer-to-peer**   :- Each node in the service discovery cluster shares the state of a service instance

3) **Load balanced**

4) **Resilient** :- The service discovery’s client should cache service information
locally. Local caching allows for gradual degradation of the service discovery
feature so that if the service discovery service becomes unavailable, applications
can still function and locate the services based on the information maintained
in their local cache
 
 5) **Fault Tolerant** :- Service discovery needs to detect when a service instance isn’t
healthy and remove that instance from the list of available services that can take
client requests.



## Why  service discovery instead of dns_resolution.
![[traditional_dns_resolved_application.png]]
<div style="color:green">image for dns resolution</div>

Why the load balancers does not work?
1) While the load balancer can be made highly available, it’s a single point of failure for your
entire infrastructure.
2) Centralizing your services into a single cluster of load balancers limits your ability to scale horizontally your load-balancing infrastructure across multiple servers
3) Most traditional load balancers are statically managed.
4) Because a load balancer acts as a proxy to the services, service consumer requests need to have them mapped to the physical services.

(By the big service discovery mafia)





#microservice  #service_discovery  #microservice_pattern 