
## Circuit breaker with resilence 4j
![[circuit-breaker.png]]



Also, in the Resilience4j circuit breaker pattern, you can define the following additional states. It is important to note that the only way to exit from the following states is to reset the circuit breaker or trigger a state transition:
-  DISABLED—Always allow access
-  FORCED_OPEN—Always deny access

Circuit breaker can be used in service calls as well as database calls.
![[resilency_wrapping 1.png]]


```java
public class licenseService{

	@CircuitBreaker(name="licenseService")  
	public List<License> getLicenseByOrganisation(String organisationId){  
	    return licenseRepository.findByOrganisationId(organisationId);  
	}
}
```


```java
@CircuitBreaker(name = "organizationService")
private Organization getOrganization(String organizationId) {
return organizationRestClient.getOrganization(organizationId);
}

```

these have different to indicate where the errors are.

``` yml

resilience4j:  
  circuitbreaker:  
    instances:  
      licenseService:  
        registerHealthIndicator: true  
        ringBufferSizeInClosedState: 5  
        ringBufferSizeInHalfOpenState: 3  
        waitDurationInOpenState: 10s  
        failureRateThreshold: 50  
        recordExceptions:  
          - org.springframework.web.client.HttpServerErrorException  
          - java.io.IOException  
          - java.util.concurrent.TimeoutException  
          - org.springframework.web.client.ResourceAccessException  
      organisationService:  
        registerHealthIndicator: true  
        ringBufferSizeInClosedState: 6  
        ringBufferSizeInHalfOpenState: 4  
        waitDurationInOpenState: 20s  
        failureRateThreshold: 60

```




![[circuit_breaker_application_yml.png]]

#spring  #spring_resilency 