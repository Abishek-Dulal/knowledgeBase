```yml

version: <docker-compose-version>
services:
  database:
	image: <database-docker-image-name>
	ports:
		- "<databasePort>:<databasePort>"
	environment:
		POSTGRES_USER: <databaseUser>
		POSTGRES_PASSWORD: <databasePassword>
		POSTGRES_DB:<databaseName>
 
  <service-name>:
	image: <service-docker-image-name>
	ports:
		- "<applicationPort>:<applicationPort>"
	environment:
		PROFILE: <profile-name>
		DATABASESERVER_PORT: "<databasePort>"
	container_name: <container_name>
	networks:
		backend:
		aliases:
			- "alias"
networks:
	backend:
		driver: bridge

```

### Docker  compose command sample.

docker-compose -f  myfile.yml  up


![[dockercompose_commands.png]]


### Reference
![[docker_refrence.png]]




### Advanced

![[docker_compose_advanced.png]]