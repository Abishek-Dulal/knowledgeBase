# Microservice Resilency patterns



![[microservice resilence pattern.png]]

Why resilency patterns:-
 1) Service degradation can start out as intermittent and then build momentum.
 2) Calls to remote services are usually synchronous and don’t cut short a long-running call.
 3) Applications are often designed to deal with complete failures of remote resources, not partial degradations.

Concept for service resilency patterns are as
1) **Client Side load balancing** :- 
	 When a service consumer needs to call a service instance, the client-side load bal-ancer returns a location from the pool of service locations it maintains. Because the client-side load balancer sits between the service client and the service consumer, the load balancer can detect if a service instance is throwing errors or behaving poorly. If the client-side load balancer detects a problem, it can remove that service instance from the pool of available service locations and prevent any future calls from hitting that service instance.
	 
2) **Circuit Breaker** :-
	when a remote service is called, the circuit breaker monitors the call. If the calls take too long, the circuit breaker intercedes and kills the call. The circuit breaker pattern also monitors all calls to a remote resource, and if enough calls fail, the circuit breaker implementation will “pop,” failing fast and preventing future calls to the failing remote resource.

3) **Fallback** :-
	With the fallback pattern, when a remote service call fails, rather than generating an exception, the service consumer executes an alternative code path and tries to carry out the action through another means. This usually involves looking for data from another data source or queueing the user’s request for future processing. The user’s call is not shown an exception indicating a problem, but they can be notified that their request will have to be tried later.

4) **Bulkheads**
	The thread pools act as the bulkheads for your service. Each remote resource is segregated and assigned to a thread pool. If one service is responding slowly, the thread pool for that type of service call can become saturated and stop processing requests. Assigning services to thread pools helps to bypass this type of bottleneck so that other services won’t become saturated.
	*service are isolated based on the thread pool*



## Failure  due to slow service.
![[resilency_failure.png]]

	
Scenario for the serivice with circuit breaker 
![[secenario_for_service_resilency.png]]


with circuit breaker we can:-
 1) Fail fast
 2) Fail gracefully
 3) Recovery Seamlessly


#microservice  #microservice_pattern #spring_resilency 