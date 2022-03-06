# Building spring app using maven docker plugin.

if you are getting permission denied use:-

```shell
sudo chmod 666 /var/run/docker.sock
```

we can use different approach to use docker in  java project:-
 1) [[dockerfile maven plugin]]
 2) [[buildpack && jib]]
 3) [[Layered Jar ]]
 4) Use dockerfile directly with docker commands.

Finally  we can use docker compose to run and coordinate services.
``` yml
version: 3.7

services:
	licensingservice:
		image: ostock/licensing-service:0.0.1-SNAPSHOT
		ports:
			- "8080:8080"
		environment
			- "SPRING_PROFILES_ACTIVE=dev"
	networks:
		backend:
			aliases:
				- "licenseservice"
networks:
	backend:
		driver: bridge
		


```


#spring #docker 