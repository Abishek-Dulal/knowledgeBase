
## Bulkhead Pattern 

The bulkhead pattern segregates remote resource calls in their own thread pools so that a single misbehaving service can be contained and not crash the container. Resilience4j provides two different implementations of the bulkhead pattern. You can use these implementations to limit the number of concurrent executions:
1) Semaphore bulkhead: Uses a semaphore isolation approach, limiting the number of concurrent requests to the service. Once the limit is reached, it starts rejecting requests.
2) Thread pool bulkhead: Uses a bounded queue and a fixed thread pool. Thisapproach only rejects a request when the pool and the queue are full.

**Default Semaphore Pattern**

![[default_semaphore_pattern.png]]

All services stop by a single service so we can have individual service management as:-
![[thread_management.png]]

```yml


resilience4j:
  bulkhead:
    instances:
      bulkheadLicenseService:
        maxWaitDuration: 10ms
        maxConcurrentCalls: 10
  thread-pool-bulkhead:
    instances:
      bulkheadLicenseService:
        maxThreadPoolSize: 1
        coreThreadPoolSize: 1
        queueCapacity: 1
        keepAliveDuration: 20ms

```
![[bulkhead_ynl.png]]

proper formula for bulkhead:-
(requests per second at peak when the service is healthy * 99th percentile latency in
seconds) + small amount of extra threads for overhead


```java

    @CircuitBreaker(name="licenseService",
            fallbackMethod = "buildFallbackLicesenList"
    )
    @Bulkhead(name="bulkheadLicenseService",
         fallbackMethod = "buildFallbackLicesenList"
    )
    public List<License> getLicenseByOrganisation(String organisationId){
        return licenseRepository.findByOrganisationId(organisationId);
    }

```
 if we want to thread pool instead of semaphore.
``` java

@Bulkhead(name="bulkheadLicenseService",  
 type = Bulkhead.Type.THREADPOOL,  
 fallbackMethod = "buildFallbackLicesenList"  
)

```



#spring  #spring_resilency 