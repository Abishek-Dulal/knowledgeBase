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



#docker 