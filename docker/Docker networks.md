The Docker networks allow us to attach the containers to as
many networks as we like. We can see the networks as a means to communicate
with isolated containers. Docker contains the following five network driver
types: bridge , host , overlay , none , and macvlan


docker running on same network can work with container name instead of the 
port and host.


if you are docker then using hostname:-
``` yml 
    environment:
      - "SPRING_PROFILES_ACTIVE=dev"
      - "SPRING_CONFIG_IMPORT= configserver:http://host.docker.internal:8071"
    extra_hosts:
      - "host.docker.internal:host-gateway"

```