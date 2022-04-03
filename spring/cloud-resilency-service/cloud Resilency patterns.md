
# Resilence4j

Resilience4j is a fault tolerance library inspired by Hystrix. It offers the following patterns for increasing fault tolerance due to network problems or failure of any of our multiple services:
1) Circuit breaker—Stops making requests when an invoked service is failing
2)  Retry—Retries a service when it temporarily fails
3) Bulkhead—Limits the number of outgoing concurrent service requests to avoid overload
4) Rate limit—Limits the number of calls that a service receives at a time
5) Fallback—Sets alternative paths for failing requests

**Execution order for resilence4j** 
Retry ( CircuitBreaker ( RateLimiter ( TimeLimiter ( Bulkhead ( Function ) )) ) )

Use Aop for execution warps the function to call them.


For Getting started with resilence4j is as
```xml

<dependency>
	<groupId>io.github.resilience4j</groupId>
	<artifactId>resilience4j-spring-boot2</artifactId>
	<version>${resilience4j.version}</version>
</dependency>
<dependency>
	<groupId>io.github.resilience4j</groupId>
	<artifactId>resilience4j-circuitbreaker</artifactId>
	<version>${resilience4j.version}</version>
</dependency>
<dependency>
	<groupId>io.github.resilience4j</groupId>
	<artifactId>resilience4j-timelimiter</artifactId>
	<version>${resilience4j.version}</version>
</dependency>
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-aop</artifactId>
</dependency>


```


There are multiple cloud resilency as:-
 1) [[circuit_breaker_pattern]]
 2) [[fallback_pattern]]
 3) [[Bulkhead_pattern]]
 4) [[Retry_pattern]]
 5) [[Rate_limitter_pattern]]


So we can use a [[user context]] to set the headers and add all the correllation information. 







#spring  #spring_resilency 
