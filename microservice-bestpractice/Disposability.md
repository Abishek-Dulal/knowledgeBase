# Disposability
Microservices are disposable and **can start and stop on demand** in order to facilitate
elastic scaling and to quickly deploy application code and configuration changes. Ide-
ally, startup should last a few seconds from the moment the launch command exe-
cutes until the process is ready to receive requests.
What we mean by disposable is that we can **remove failing instances with new
instances** without affecting any other services. For example, if one of the instances of
the microservice is failing because of a failure in the underlying hardware, we can shut
down that instance without affecting other microservices and start another one some-
where else if needed.





#microservice  #bestpractise 