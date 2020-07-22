## 1. Understanding the need for a system like Kubernetes
* Monolithic applications consist of components that are all tightly coupled together and have to be developed, deployed, and managed as one entity, because they all run as a single OS process.
* Changes to one part of the application require a redeployment of the whole application, and over time the lack of hard boundaries between the parts results in the increase of complexity and consequential deterioration of the quality of the whole system because of the unconstrained growth of inter-dependencies between these parts.
* Running a monolithic application usually requires a small number of powerful servers that can provide enough resources for running the application.
* To deal with increasing loads on the system, you then either have to vertically scale the servers (also known as scaling up) by adding more CPUs, memory, and other server components, or scale the whole system horizontally, by setting up additional servers and running multiple copies (or replicas) of an application (scaling out).
* While scaling up usually doesn’t require any changes to the app, it gets expensive relatively quickly and in practice always has an upper limit.
* Scaling out, on the other hand, is relatively cheap hardware-wise, but may require big changes in the application code and isn’t always possible—certain parts of an application are extremely hard or next to impossible to scale horizontally (relational databases, for example).
* If any part of a monolithic application isn’t scalable, the whole application becomes unscalable, unless you can split up the monolith somehow.

### SPLITTING APPS INTO MICROSERVICES
* These and other problems have forced us to start splitting complex monolithic applications into smaller independently deployable components called microservices.
* Each microservice runs as an independent process and communicates with other microservices through simple, well-defined interfaces (APIs).
* Microservices communicate through synchronous protocols such as HTTP, over which they usually expose RESTful (REpresentational State Transfer) APIs, or through asynchronous protocols such as AMQP (Advanced Message Queueing Protocol).
* These protocols are simple, well understood by most developers, and not tied to any specific programming language.
* Each microservice can be written in the language that’s most appropriate for implementing that specific microservice.
* Because each microservice is a standalone process with a relatively static external API, it’s possible to develop and deploy each microservice separately.
* A change to one of them doesn’t require changes or redeployment of any other service, provided that the API doesn’t change or changes only in a backward compatible way.

### SCALING MICROSERVICES
* Scaling microservices, unlike monolithic systems, where you need to scale the system as a whole, is done on a per-service basis, which means you have the option of scaling only those services that require more resources, while leaving others at their original scale.
* Certain components are replicated and run as multiple processes deployed on different servers, while others run as a single application process.
* When a monolithic application can’t be scaled out because one of its parts is unscalable, splitting the app into microservices allows you to horizontally scale the parts that allow scaling out, and scale the parts that don’t, vertically instead of horizontally.

### DEPLOYING MICROSERVICES
* As always, microservices also have drawbacks.
* When your system consists of only a small number of deployable components, managing those components is easy.
* It’s trivial to decide where to deploy each component, because there aren’t that many choices.
* When the number of those components increases, deployment-related decisions become increasingly difficult because not only does the number of deployment
combinations increase, but the number of inter-dependencies between the components increases by an even greater factor.
* Microservices perform their work together as a team, so they need to find and talk to each other
* When deploying them, someone or something needs to configure all of them properly to enable them to work together as a single system.
* With increasing numbers of microservices, this becomes tedious and error-prone, especially when you consider what the ops/sysadmin teams need to do when a server fails.
* Microservices also bring other problems, such as making it hard to debug and trace execution calls, because they span multiple processes and machines.

### UNDERSTANDING THE DIVERGENCE OF ENVIRONMENT REQUIREMENTS
* As I’ve already mentioned, components in a microservices architecture aren’t only deployed independently, but are also developed that way.
* Because of their independence and the fact that it’s common to have separate teams developing each component, nothing impedes each team from using different libraries and replacing them whenever the need arises.
* The divergence of dependencies between application components, where applications require different versions of the same libraries, is inevitable.
* Deploying dynamically linked applications that require different versions of shared libraries, and/or require other environment specifics, can quickly become a nightmare for the ops team who deploys and manages them on production servers.
* The bigger the number of components you need to deploy on the same host, the harder it will be to manage all their dependencies to satisfy all their requirements.

## 2. Moving from monolithic apps to microservices
## 3. Providing a consistent environment to applications
## 4. Moving to continuous delivery: DevOps and NoOps

## 5. Introducing container technologies
## 6. 1Understanding what containers are
## 7. Introducing the Docker container platform

## 8. Introducing Kubernetes
## 9. Understanding its origins
## 10. Looking at Kubernetes from the top of a mountain
## 11. Understanding the architecture of a Kubernetes cluster
## 12. Running an application in Kubernetes
## 13. Understanding the benefits of using Kubernetes

## Summary
