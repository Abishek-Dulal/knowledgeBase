# Config 

![[Config.png]]


This practice refers to how you store your application configurations (especially your
environment-specific configurations). Never add embedded configurations to your
source code! Instead, it’s best to maintain your configuration completely separate
from your deployable microservice

## Best practice for config management
- Completely separate the configuration of an application from the actual code
being deployed.
- Build immutable application images that never change as these are promoted
through your environments.
- Inject any application configuration information at server startup through
either environment variables or a centralized repository that the microservices
read on startup



## microservice config strategy
- **Segregate** : complete seperate configuration from  service.
- **Abstract**: use a proper intrefact to retrieve microservice logs.
- **Centralise** : centralise the config in a single repository
- **Harden**: Use highly available and redundant.
![[config_processing_archietecture.png]]


Tech option for configuration are:-
- Eureka server
- etcd
- consul
- zookeeper
- spring Cloud Configuration.



#microservice  #bestpractise 