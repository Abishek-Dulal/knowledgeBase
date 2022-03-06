# How to build a [[docker]] file
![[dockerfile_cheatsheat.png]]

we also have
 <div style="color: orange;font-weight:bold">ENV: username=admin \ <br>
 password= 123234

</div>

``` dockerfile
FROM node:12-alpine
RUN apk add --no-cache python2 g++ make
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000

```


```bash
docker build -t my-app:1.0 

```


We can also have multistage file to reduce file size.
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




#docker 