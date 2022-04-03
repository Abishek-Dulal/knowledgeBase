
the pom xml  :-

``` xml
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>

```


for the application yml

```properties
management.endpoints.web.exposure.include=*  
management.endpoints.enabled-by-default=true  
  
eureka.instance.preferIpAddress = true  
eureka.client.registerWithEureka = true  
eureka.client.fetchRegistry = true  
eureka.client.serviceUrl.defaultZone = http://localhost:8070/eureka/  
eureka.client.enabled = true
```

Java with discovery client and  
``` java 
@SpringBootApplication  
@EnableDiscoveryClient  
@EnableFeignClients  
@RefreshScope  
public class LicenseserverApplication {  
  
    public static void main(String[] args) {  
        SpringApplication.run(LicenseserverApplication.class, args);  
 }  
  
    @Bean  
 @LoadBalanced public RestTemplate getRestTemplate(){  
        return new RestTemplate();  
 }  
  
}

```


For using discovery client :-

```java
@Component  
public class OrganisationDiscoveryClient {  
  
    @Autowired  
 private DiscoveryClient discoveryClient;  
  
  
 public Organization getOrganisation(String organisationId){  
    RestTemplate restTemplate = new RestTemplate();  
    List<ServiceInstance> instances = discoveryClient.getInstances("organization-service");  
 if (instances.size()==0 )  
            return null;  
		 String serviceUri = String.format("%s/v1/organization/%s",instances.get(0).getUri().toString(),organisationId);  
  
 ResponseEntity<Organization> exchange = restTemplate.exchange(serviceUri, HttpMethod.GET, null, Organization.class, organisationId);  
 return exchange.getBody();  
 }
}








```


Using Feign client

``` java

@FeignClient("Organisation-service")  
public interface OrganisationFeignClint {  
  
    @RequestMapping(  
            method = RequestMethod.GET,  
 value="/v1/orgaization/{organisationId}",  
 consumes = "application/json")  
    Organization getOrganisation(@PathVariable("organisationId") String organisationId);
}


```


Using rest template:-

``` java
@FeignClient("Organisation-service")  
public interface OrganisationFeignClint {  
  
    @RequestMapping(  
            method = RequestMethod.GET,  
 value="/v1/orgaization/{organisationId}",  
 consumes = "application/json")  
    Organization getOrganisation(@PathVariable("organisationId") String organisationId);

```




#spring #service_discovery 










#spriing #service_discovery 