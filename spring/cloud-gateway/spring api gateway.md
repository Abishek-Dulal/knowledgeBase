![[how_gateway_works.png]]# What is the api gateway
A service gateway acts as an intermediary between the service client and an invoked
service. The service client talks only to a single URL managed by the service gateway.
The service gateway pulls apart the path coming in from the service client call and
determines what service the service client is trying to invoke
![[api_gateway_working.png]]

What is service api gateway may be useful for:-
1) Static routing :-   ex. single top level domain for usage.
2) Dynamic routing :-  ex.  beta user to beta cluster
3) Authentication and Authorisation  
4) Metric collection and logging 


Api gateway as a chokepoint service:-
- Keep any code you write for your service gateway stateless. (don't have state information)
- Keep the code you write for your service gateway light. (no multiple db calls )
- Load balancers are useful when placed in front of individual groups of services. ( not for all the services)

## Why Spring cloud gateway
1) Mapping the routes for all the services in your application to a single URL
2) Building filters that can inspect and act on the requests and responses coming through the gateway.
3) Building predicates, which are objects that allow us to check if the requests fulfill a set of given conditions before executing or processing a request.

``` xml
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-gateway</artifactId>
        </dependency>
```


Spring routing mechanism:-
1) Automated mapping of routes using service discovery
2) Manual mapping of routes using service discovery

## Automated Mapping 
route mapping can be done from this file.
```
/src/main/resources/config/gateway-server.yml

```

```yml
spring:
	gateway:  
	  discovery:  
	    locator:  
	      enabled: true  
	      lower-case-service-id: true
```



![[gateway_enable_yml.png]]

	![[gateway_with_euraka.png]]

path for routes in api gateway.

```
http://{{basepath}}/actuator/gateway/routes
```


## Manually mapping  routes using service ![[manual_api_gateway_yml.png]]



```
spring:
	gateway:  
	  routes:
		- id: organisation-service  
	    uri: lb://organization-service  
	    predicates:  
	      - Path=/organisation/**  
	    filters:  
	      - RewritePath=/organization/(?<path>.*), /$\{path}


```

Routes are refreshed by the path
```
http://{{basepath}}/actuator/gateway/refresh
```
![[how_gateway_works.png]]


## Built in predicate
![[api_gateway_fileres1.png]]


![[api_gateway_filter2.png]]


## Built in filter

![[gateway_predicate_1.png]]


![[gateway_predicate_2.png]]


## Custom filters

![[spring_gateway_filters.png]]


 ### our custom filter
 ![[setting_correlation_service.png]]



Custom post filter.
``` java
@Configuration
public class ResponseFilter {

    final Logger logger = LoggerFactory.getLogger(ResponseFilter.class);

    @Autowired
    FilterUtils filterUtils;

    @Bean
    public GlobalFilter postGlobalFilter(){
        return ((exchange, chain) -> chain.filter(exchange).then(Mono.fromRunnable(()->{
                HttpHeaders requestHeaders = exchange.getRequest().getHeaders();
                String correlationId = filterUtils.getCorrelationId(requestHeaders);
                logger.debug("Adding the correlation id  to the outbound header {}", correlationId);
                exchange.getResponse().getHeaders().add(FilterUtils.CORRELATION_ID,correlationId);
                logger.debug("Completing  outgoing  request {}", exchange.getRequest().getURI());
            }))
        );
    }

}



```




#spring #api_gateway