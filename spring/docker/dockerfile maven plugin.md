# Docker can be used in spring with dockerfile plugin as:-

we just need to add the docker file plugin :-

```xml

            <plugin>
                <groupId>com.spotify</groupId>
                <artifactId>dockerfile-maven-plugin</artifactId>
                <version>1.4.13</version>
                <configuration>
	                    <repository>${docker.image.prefix}/${project.artifactId} 
                        </repository>
                    <tag>${project.version}</tag>
                    <buildArgs>
                        <JAR_FILE> target/${project.build.finalName}.jar</JAR_FILE>
                    </buildArgs>
                </configuration>
                <executions>
                    <execution>
                        <id>default</id>
                        <phase>install</phase>
                            <goals>
                                <goal>build</goal>
                                <goal>push</goal>
                            </goals>
                    </execution>
                </executions>
            </plugin>




```
 
 for further information:-
	https://github.com/spotify/dockerfile-maven

Multistage docker file for spring project.

```Dockerfile
FROM openjdk:17-alpine as build  
ARG JAR_FILE  
COPY ${JAR_FILE} app.jar  
RUN mkdir -p target/dependency && (cd target/dependency; jar -xf ../../app.jar)  
FROM openjdk:17-alpine  
VOLUME /tmp  
ARG DEPENDENCY=/target/dependency  
COPY --from=build ${DEPENDENCY}/BOOT-INF/lib /app/lib  
COPY --from=build ${DEPENDENCY}/META-INF /app/META-INF  
COPY --from=build ${DEPENDENCY}/BOOT-INF/classes /app  
ENTRYPOINT ["java","-cp","app:app/lib/*","com.optimagrowth.licenseserver.LicenseserverApplication"]

```


#spring  #docker 