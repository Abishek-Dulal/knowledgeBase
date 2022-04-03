![[licensing_service_service_discovery.png]]

## Setting the Service Discovery
we are setting creating the eureaka server with  spring load balancer instead of eureka .

```xml
<dependency>  
 <groupId>org.springframework.cloud</groupId>  
 <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>  
 <exclusions> 
	 <exclusion> 
		 <groupId>org.springframework.cloud</groupId>  
		 <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>  
	 </exclusion> 
	 <exclusion> 
		 <groupId>com.netflix.ribbon</groupId>  
		 <artifactId>ribbon-eureka</artifactId>  
	 </exclusion> 
 </exclusions>
</dependency>
```

Load Balancer dependency.
```xml
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-loadbalancer</artifactId>
        </dependency>
```

application  properties needed:-
```yml
spring:
  application:
    name: eureka-server
  config:
    import: configserver:http://127.0.0.1:8071
  cloud:
    loadbalancer:
      ribbon:
        enabled: false

```

```java
@SpringBootApplication  
@EnableEurekaServer  
public class EurekaserverApplication {  
  
    public static void main(String[] args) {  
        SpringApplication.run(EurekaserverApplication.class, args);  
 }  
  
}

```

Additional application configs are:
 ```yaml
server:  
  port: 8070  
  waitTimeInMsWhenSyncEmpty: 5  
  
eureka:  
  instance:  
    hostname: localhost  
  client:  
    register-with-eureka: false  
    fetch-registry: false  
    service-url:  
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/
 
 
 ```

for the client look at [[Service discovery client]]


#spring #service_discovery 