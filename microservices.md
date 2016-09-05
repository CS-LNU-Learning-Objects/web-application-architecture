# Introduction to microservices

*Prior  knowledge  - Programming, Web development*

The purpose of this text is to be a introduction to the term microservice and get a clue why and how it is used in web development.

## Web Application architecture
As a web developer you will see that it will be many ways to build the architecture for your web application. When we talk about architecture we mean that we are looking at the application at a higher level then just how to write code or which programming language that will be used. We rather concentrate on how the application and its data management should look like. How all the bigger parts of a complex application/system should be connected and fit together.

We know that this is hard cause the application is a living thing that will get new requirements on functionality and probably evolve from a small application to a bigger more complex application with (preferable) more traffic then we expect from the beginning. We need to architect our application so it will be easy to add and change functionality and handle scalability in a good way. Web application architecture is a big topic and there are many ideas and research done in this subject.

Often when we build web applications, we do it in a monolithic way. This means that the application and all of it code was one big thing, maybe one big file running on one  server as a single unit. Maybe as a WAR or JAR file or a web application project including code doing all the things. When we need to change the application and build more features this unit become bigger and bigger and it gets harder and harder to make these changes. This may work when handling smaller applications but when the complexity gets bigger we need to rethink.

### N-layer applications
This led to new web application architectures where we tried to split the application code into different layers to separate things. You often talk about the **three-layered architecture** where each layer has its own responsibility (compare to network technologies with there OSI- and TCP/IP models of layers). Each layer should be as independent as possible to make it possible to change the code in the layer and not mess up the whole application.

![three-layered](https://github.com/CS-LNU-Learning-Objects/web-application-architecture/raw/master/images/three-layer.png)

The presentation layer (UI) is responsible for the code rendering the client side and the client logic. The business layer had all the rules for the application and took the input from the presentation and communicate with the below data access layer. This layer communicates with the database, reading and writing the data in a persistent way. This lead to a better separation of concern and made it a little bit better to more effective scalability. But it's still a monolithic application.

The problem is still that the application is one big unit with all its functionality. The scale problem is often solved this by using a load balancer and multiple instances of the application to split the traffic over several applications.

Of course you are not bound to use just three layers. In some cases you may want to separate the code more or maybe add a layer such as an API layer generating data in standard format such as JSON or XML. This could still lead to complex applications, that is hard to work with and hard to scale. This is called **n-layer architecture**.

### SOA - Service Oriented Architecture
We tried to solved this by also splitting applications horizontally not only vertical. Instead of talking about single unit applications we were trying to build applications with different separated services that could collaborate together. The services can be run in separate operating systems so they easily can be scaled in one or more servers. This mean a more physical separation that not was intended with the n-layer architecture (even if this could work in that architecture also).

The industry start to develop standards like the [Web Service stack](https://www.w3.org/TR/2002/WD-ws-arch-20021114/) and this became a big hit in the enterprise segment. This was often called [Software Oriented Architecture (SOA)](https://en.wikipedia.org/wiki/Service-oriented_architecture).
The problem was that this got very complex and very hard to follow a good practice how to develop real-world applications (some will say it was more enterprise then real-world developing). The idea to split a big application to smaller bits was good but what is enough small...or big and how would all these standards and protocol fit in real-world scenarios? This led to many pitfalls even though we should remember that many enterprise solution still today is build on these techniques.

### Microservices
The SOA idea is still a good idea but it needed a rethinking where focus on real-world problems with an understanding of how architectures and systems work. A reaction to the complex enterprise part of SOA, the microservice definition, was born. You should see this definition as an approach to SOA, just like SCRUM is an approach to agile development.

In a microservice scenario the application is composed by smaller independent services and its data is exposed by an API, preferable with common web friendly exchange formats like JSON or web sockets (The WS-* standard was focusing on XML). This is the only connection between the services and is also the protocol in which services can communicate with each other. This philosophy is much like the one in the Linux community where the system is built on small program (good at what they are doing) with a output that can be piped to another program to accomplish more complex tasks. In a web application scenario this will lead to a more easily and more precise scaling among other advantages.

![microservice](https://github.com/CS-LNU-Learning-Objects/web-application-architecture/raw/master/images/microservice.png)

The image above try to show how a web application (web shop) is separated to three independent services only reachable through an API. The client application communicates through the APIs and the APIs can communicate internal. We have more separations of concern making it easier to add functionality and scale more effective.

In most cases when we are talking about microservices we are talking about back-end services that returns data in a pleasant format like JSON. This means that client applications (applications running in the browser) often consume data from one or more services and put it together in monolithic way in a so called single page application (SPA). Maybe the future holds a more microservice-way of looking in front-end developing through technologies like [web components](http://webcomponents.org)

#### Advantages
If we look at the scaling we can now easy scale up that part of the application that is needed to scale. We are probably getting more requests to our shop-service than to the user management service. It is more effective to run multiple instances of that shop service than running a whole monolithic application just for scaling that part of the application.

 When we develop more independent services we also have more space for innovation. Trying new features in a monolithic application is often hard and complicated, we are bound to a specific technology and program language. If we are using a more service separated approach we can have different teams working on different services, with different technologies. We can also choose the best tool for the task, maybe nodeJS is better for some kind of services and Python for another. We can also follow the technology changes (new frameworks for example) when developing new services.

A smaller service is also more understandable. It is easier to get a grip what the service is doing and this also cut the need for documentation. Even if you´re not used to the programming language you should get a grip of what the service does. It is also easier for newcomers to jump into the code in a smaller service.

Another good thing is that it easy to deploy and put the specific service into  (especially with [software containers](https://en.wikipedia.org/wiki/Operating-system-level_virtualization)). We also have better control when we need to rollback a problem or fault isolation. Smaller parts will be easier to test since they have a clear responsibility.

#### Disadvantages
So this microservice thinking is a silver bullet? Well as you probably know by now there are no silver bullets in software development. As you probably notice when we building smaller application in the service oriented way there will be more application and probably more servers to operate and install then when using the monolithic way. This was maybe a bigger problem before the rise of virtualization and the ability to work with containers. For more information about this see the paper on [containers/docker](https://github.com/CS-LNU-Learning-Objects/web-application-architecture/blob/master/containers.md)

A monolithic application will always have better performance. The internal calls in the application goes through the internal code and this will be faster then API calls. The services will have to make lots of request to each other to communicate and become the whole application. Today we probably have fast internal LAN and maybe the problem don´t would be so big but in some rare cases it will be a concern.

The biggest problem is still how to split the application and which parts should be a services. Often you specify a service as a handler of a feature or a specific function in a application. In many cases it can be hard to see the clear line of what should be a service.

### Resourses

Martin Fowler is a design pattern guru. Here is an article about microservices written by him and James Lewis - A must read: http://martinfowler.com/articles/microservices.html
