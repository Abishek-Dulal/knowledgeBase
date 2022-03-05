# Devops handles the operation of the microservices.

The principle of microservice devlopment defined :-
1) A microservice should be self-contained.
2) A microservice should be configurable
3) A microservice instance needs to be transparent to the client.
4) A microservice should communicate its health.

From the devops prespectice  standard set of lifecycle events :-
 1) Service assembly

![[assembly.png]]
mvn clean package && java -jar target/licensing-service-0.0.1-SNAPSHOT.jar
 2) Service bootstrapping
![[service_bootstrap.png]]
 3) Service registration
![[service_registration.png]]

 5) Service monitoring
 ![[service_monitoring.png]]
  

<div style=" color:green;font-weight:bold">Complete Flow for Service developement.</div>
![[devops_operation.png]]


