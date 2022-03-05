# Role of Software Archietect

 <div style="font-weight:bold">1)   Decomposing the business problem </div>
      - Describe the business problem and notice the nouns you use to describe it.
      - Pay attention to the verbs
      - Look for data cohesion. 
     <div style="color:green"> Looking at  the model defines data base </div>
    ![[monolith_model.png]]
	<div style="color:green">Simplifying the design for microservice</div>
![[microservice_model.png]]
<div style= "font-weight:bold">2) Establishing service granularity</div>
	![[microservice_granuality.png]]

How to find the right level  for service granuality:-
1) it’s better to start broad with our microservice and refactor to smaller services.
2) Focus first on how our services interact with one another.
3) Service responsibilities change over time as our understanding of the problem domain
grows

When is Service too big :-
- A service with too many responsibilities.
-  A service that manages data across a large number of tables.
-  A service with too many test cases.

When is Service too Small:-
-  The microservices in one part of the problem domain breed like rabbits
-  Your microservices are heavily interdependent on one another.
-  Your microservices become a collection of simple CRUD

3) Defining the service interfaces
	- Embrace the REST philosophy
    - Use URIs to communicate intent.
    - Use JSON for your requests and responses.
    - Use HTTP status codes to communicate results. 


#microservice  