# Config for vault
``` yml
profiles:
  active:  git,vault
cloud:
  config:
    server:
      bootstrap: true
      vault:
        port: 8200
        host: localhost
        order: 1
        kvVersion: 2
        authentication: TOKEN
        token: myroot
        scheme: http
        skipSslValidation: true
```
The authentication method  can be changed and in production should be changes.

Docker config for the data :-
 ```yml
services:
  config-server:
    image: ostock/configserver:0.0.1-SNAPSHOT
    ports:
      - "8071:8071"
    networks:
      backend:
    depends_on:
      - vault-server
  vault-server:
    image: vault:latest
    ports:
      - "8200:8200"
    environment:
      - "VAULT_DEV_ROOT_TOKEN_ID=myroot"
      - "VAULT_DEV_LISTEN_ADDRESS=0.0.0.0:8200"
    networks:
      backend:
 ```

communicating with the vault data ui:-

http://localhost:8200/ui/vault/auth?with=token

so the config are kept in :-
  secret > licenseserver
  secret > licenserver,dev (the path is specified with comma)
  