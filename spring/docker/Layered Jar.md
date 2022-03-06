
 ### Layered Jar

 Add first the spring plugin code.
 
```xml

<plugin>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-maven-plugin</artifactId>
	<configuration>
		<layers>
		<enabled>true</enabled>
		</layers>
	</configuration>
</plugin>


```

then we can do this

```bash
mvn clean package
```

Once the JAR file is created, we can execute the following command in the root direc-
tory of our application to display the layers and the order in which these should be
added to our Dockerfile:

```bash
java -Djarmode=layertools -jar target/licensing-service-0.0.1-SNAPSHOT.jar list

```
Output of the above  command is :-

 <ul>
     <li>dependency</li>
<li>spring-boot-loader</li>
<li>snapshot-dependencies</li>
<li>application</li>
</ul>
Now we can build docker file 

```Dockerfile
FROM openjdk:11-slim as build
WORKDIR application
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} application.jar
RUN java -Djarmode=layertools -jar application.jar extract

FROM openjdk:11-slim
WORKDIR application
COPY --from=build application/dependencies/ ./
COPY --from=build application/spring-boot-loader/ ./
COPY --from=build application/snapshot-dependencies/ ./
COPY --from=build application/application/ ./
ENTRYPOINT ["java", "org.springframework.boot.loader.JarLauncher"]



```

run this file for docker file.

```shell
docker build . --tag licensing-service
docker run -it -p8080:8080 licensing-service:latest
```

#spring #docker 