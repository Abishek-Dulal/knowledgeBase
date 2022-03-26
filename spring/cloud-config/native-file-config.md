# Configuration for file based config

```yml
spring:
  application:
    name: config-server
  profiles:
    active: composite
  cloud:
    config:
      server:
        composite:
          - type: native
            search-locations: classpath:\config
        bootstrap: true

management:
  health:
    defaults:
      enabled: true

server:
  port: 8071

```

## native is  profile in spring cloud  indicating it is loading configuration from files .

so to load from configuration
``` yml
	search-locations: classpath:\config   
```