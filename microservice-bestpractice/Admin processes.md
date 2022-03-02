# Admin Processes 

Developers will often have to do administrative tasks for their services (data migration
or conversion, for example). These tasks should **never be ad hoc and instead should
be done via scripts** that are managed and maintained through a source code
repository. The scripts should be repeatable and non-changing **(the script code isn’t
modified for each environment)** across each environment they’re run against. It’s
important to have defined the types of tasks we need to take into consideration while
running our microservice, so that if we have multiple microservices with these scripts,
we are able to execute all of the administrative tasks without having to do this
manually.

Main points:-
 1) Automate all the admin process.
 2) never have ad hoc process.
 3) use script and save them in repository.


#microservice  #bestpractise 