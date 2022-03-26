# Spring cloud config
bootstrap.yml file is loaded first before application.properties file in spring cloud config.


To use cloud config we do:-

``` java
@EnableCloudConfig
@SpringBootApplication
public class ServerApplication{

}

```

Config can be applied using:
[[git file config]]
[[native-file-config]]
[[vault cloud config]]



Spring pom file for the spirng cloud configuration on the server side is:-
```xml
<project ...>

<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>${spring-cloud.version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
 <dependencies>
      <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-config-server</artifactId>
        </dependency>
 </dependencies>

</project>

```

from the  client side we need with dependency management:

```xml
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-config</artifactId>
        </dependency>
```

``` yml
spring:
    application:
      name: licensing-service
    profiles:
      active: dev
    config:
      import: configserver:http://127.0.0.1:8071

```


if you are docker then using hostname:-
``` yml 
    environment:
      - "SPRING_PROFILES_ACTIVE=dev"
      - "SPRING_CONFIG_IMPORT= configserver:http://host.docker.internal:8071"
    extra_hosts:
      - "host.docker.internal:host-gateway"

```



Config for default configuration:-
![[cloud-config-server.png]]


Archietecture sample for spring configuration application.

![[cloud-config-working-mechanism.png]]

## Spring configuration Security .
put the property in application properties in both server and client. 

```yml
encrypt:
  key : encryptkey 

```

we can using this to encrypt 
```
[POST] {{serverurl}}/encrypt
[request]  data
[response] asdfasdlfasdf1234432
```

so finally put the data in property file as:-
``` yml
mydata: {cipher} asdfasdlfasdf1234432

```



#spring 