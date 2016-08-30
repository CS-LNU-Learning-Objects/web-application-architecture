## Introduction to microservices

*Prior  knowledge  - Programming, Web development*

The purpose of this text is to get a introduction to the term microservice and get a short image of why and how it is used in web development.

### Web Application architecture
As a web architecture there will be many ways to build the architecture for your web application. When we talk about architecture we mean that we are looking at the application in a higher level and not focusing on how to write code or which programming language you should use. We rather concentrate on how the application and it data management should look like. We know that this is hard cause the application is a living thing that will get new requirements on functionality and probably evolve from a small application to a bigger more complex application with (preferable) more traffic then we expect from the beginning. To handle this changes in a good and fast way we need to have a good architecture. Web application architecture is a big topic and there are many ideas and research done in this subject.

If we go back in time and look at the web application software development in the beginning we were building application in a monolithic way. This means that the application and all of it code was one big thing, maybe one big file running on one big server as a big single unit. Maybe as a WAR or JAR file. When we need to change the application and build more features this unit become bigger and bigger and it gets harder and harder to make these changes.

#### N-layer applications
This led to new architectures where we tried to split the application code into different layers to separate things. You often talk about the three-layered architecture where each layer has its own responsibility (compare to network technologies with there OSI- and TCP/IP models of layers). Each layer should be as independent as possible to make it possible to change the code in the layer and not mess up the whole application.

INSERT IMAGE HERE

The presentation layer was responsible for the code rendering the client side and the client logic. The business layer had all the rules for the application and took the input from the presentation and communicate with the below data access layer. This layer communicates with the database, reading and writing the data in a persistent way. This lead to a better separation of concern and made it a little bit better to develop new functionality and find bugs in the code. But it's still a monolithic application.

The problem is still that the application is one big unit and we still have problem men we need to scale the application to handle more traffic. You often solved this by using a load balancer and multiple instances of the application to split the traffic over several applications.

INSERT IMAGE HERE

Of course you was not bound to use just three layers. In some cases you maybe wanted to separate the code more or maybe ad a layer such as an API layer generating data in standard format such as JSON or XML. This could still lead to extremely complex that is hard to work with and hard to scale.

### SOA - Service Oriented Architecture
We tried to solved this by splitting the application horizontally not only vertical. Instead of talking about single unit applications we were trying to build applications with different separated services that could collaborate together. The services should be running in separate operating systems so they could easily be scaled in one or more servers. This mean a more physical separation that not was intended with the n-layer architecture (even if this could work in that architecture also). The industry start to develop standards like the [Web Service stack](#) and this became a big hit in the enterprise segment. There were standard and protocols to define how different service should be able to collaborate together in a whole application. To read more about the SOA definition see [wikipedia](#).
The problem was that this got very enterpriseing and very hard to follow a good practice how to develop real-world applications. The idea to split a big application to smaller bits was good but what is enough small...or big and how would all these standards and protocol fit in real-world scenarios? This led to many pitfalls even though we should remember that many enterprise solution still today is build on these techniques.

IMAGE OF WS-*

### Microservices
The SOA idea is still a good idea but that needed a rethinking where focus on real-world problems was in focus with an understanding of how architectures and systems work. A reaction to the complex enterprise part of SOA the microservice definition was born. You should see this definition as an approach to SOA, just like SCRUM is an approach to agile development.

In a microservice scenario the application is composed by smaller independent services and its data is exposed by an API, preferable with common web friendly exchange formats like JSON. The WS-* standard was focusing on XML. This is the only connection between the services and is also the protocol in which services can communicate with each other. This philosophy is much like the one the Linux community is using where the system is built on small program (good at what they are doing) with a output that can be piped to another program to accomplish more complex tasks. In a web application scenario this will lead to a more easily and more precise scaling among other advantages.

IMAGE HERE

#### Advantages
If we look at the scaling we can now easy scale up that part of the application that is needed to scale. We are probably getting more requests to our webshop-service than to the registration service. When we develop more independent services we also have more space for innovation. Trying new features in a monolithic application is often hard and complicated, we are bound to a specific technology and program language. If we are using a more service separated approach we can have different teams working on different services, with different technologies. We can also choose the best tool for the task, maybe nodeJS is better for some kind of services and JAVA for another. We can also follow the technology changes (new frameworks for example) when developing new services.

A smaller service is also more understandable. It is easier to get a grip what the service is doing and this also cut the need for documentation. This is also easier for newcomers to jump into the code in a smaller service. Another good thing is that it easy to deploy and put the specific service into production. We also have better control when we need to rollback a problem or fault isolation. Smaller parts will be easier to test since they have a clear responsibility.

#### Disadvantages
So this microservice thinking is a silver bullet? Well as you probably know by now there are no silver bullets in web development. As you probably notice when we building smaller application in the service oriented way there will be more application and probably more servers to operate and install then when using the monolithic way. This was maybe a bigger problem before the rise of virtualization and the ability to work with containers. For more information about this see the paper on [containers/docker](#)

A monolithic application will always have better performance. The internal calls in the application goes through the internal code and this will be faster then remote procedure calls (RPCs). The services will have to make lots of request to each other to communicate and become the whole application. Today we probably have fast internal LAN and maybe the problem don´t would be so big but in some cases (probably < 0.05%) it will be a concern.
The biggest problem is still how to split the application and what should be a service. Often you think of it as an service is handling a feature or a specific function in a application but it can be hard to se the clear line.

### Resourses

More reading:
http://martinfowler.com/articles/microservices.html
