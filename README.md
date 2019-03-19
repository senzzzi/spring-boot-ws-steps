# spring-boot-ws-steps
Aveiro's University Spring Boot Workshop Steps

## Main Purpose
End up with a production ready microservice with some simple endpoints to manage a chosen entity. Logging and Metrics should be taken in to consideration during development.

## Description
Spring Boot provides a wide set of features. With very little configuration (and code!) it is possible to create production ready microservices. You can find more info on [Spring Boot Reference Guide](https://docs.spring.io/spring-boot/docs/current/reference/html/). This workshop will show how to leverage all this configuration to create a working microservice.

## Requirements
* Java 8+
* Java IDE
* Maven
* Git

## Workshop Main Steps
### Step 1
* Start by going to [Spring Initializr](https://start.spring.io/). In this website, it is possible to create an initial version of a spring boot project. 
* As a suggestion, use Maven Project as Project, Java as Language and 2.1.3 as version. Fill project metadata as you like but the defaults work for the purpose of this workshop. As dependencies choose at least: Web, JPA, H2 and Actuator.
* Generate the project, download the zip file and import the project on your chosen IDE.
* Try to build the project and run it. 
* Make you service answer at port 8080 (check application.properties)
* If you succeed, a "Application started" message should appear on the service logs.

### Step 2
* At this point you should choose a "entity" that you want to manage. I suggest to create a simple entity, with only a id (Long type) and a value (String type e.g.). Create the corresponding class on a "model" package.
* Create a "controller" package,
* Inside this package create a Controller class (you can name it whatever you like).
* Inside the created class, create a GET endpoint (/entities) to get a list of all the entities you created. Make this endpoint return a empty list.
* You should be able to call this endpoint on host:port/path-to-your-endpoint and get a 200 OK and an empty list.

### Step 3
* Add a Logger to your Controller class. 
* Add a "info" message using the logger to your endpoint.
* Now, everytime you call the endpoint, a message should appear on your services logs (good, you now know how you can monitor your service in production)

### Step 4
* Let's add some persistence. Remember the H2 dependency? Well, this dependency automatically creates a in-memory relational database (please don't use it in production!). You will notice that whenever you restart your service. 
* Also, remember JPA? You can, only using annotations on your entity class, make the service create a table on this in-memory DB. This [JPA Guide](https://spring.io/guides/gs/accessing-data-jpa/) might be helpful.
* Check on h2-console if your table was created! (Tip: you will need to add some properties to enable the console on /h2-console path).

### Step 5
* Your endpoint is still returning an empty list!
* Create a "repository" package and inside it, a Repository interface (check CrudRepository and the guide on Step 4 might also be helpful!)
* Add your repository to your endpoint.

### Step 6
* You can manually create data on the H2 console and see that your endpoint returns the data you stored. (Because this is an in-memory DB, the data is wiped everytime you run the service)
* Check that your endpoint return real data.

### Step 7
* Create a new GET endpoint (/entities/{entityId}) to get your entity by ID (use the CrudRepository magic again, check the methods inside it).
* Check that it works before moving on.

### Step 8
* What happens if the entity you requested doesn't exist? A error should be thrown right? Maybe a 404 NOT FOUND?
* Create a custom exception to be thrown in that case, throw it in case the entity with the requested id doesn't exist.
* With a simple annotation on the exception class you can change the Response Status to 404. 
* Check that it works calling GET /entities/unexistent-id

### Step 9
* We already added logging but how can we know much memory our application is using? What about CPU? Response times? It would be cool to have some metrics about our service. Remember the Actuator dependency you added on Step 1? Find out how you can enable the actuator metrics endpoint and investigate it a little bit. There are lots of metrics out-of-the-box.
* Find out on fast your service answer one of the GET endpoints in milisseconds.

At this point your microservice is production ready (if you use a proper DB and not H2) with 2 endpoints to fetch some data.

## Bonus Steps
### Step 10
* Create a POST endpoint (/entities) to create entities on your DB

### Step 11
* Create a PUT endpoint (/entities/{entityId}) to update a entity on your DB

### Step 12
* Create a DELETE endpoint (/entities) to delete an existent entity on your DB




