This text is written to give a short introduction to containers and docker in particular. It´s mainly written from a developers point of view.

# Introduction to containers and Docker
To understand what a container is you first have to be familiar with what virtualization is. That is a technique that allows you to run independent virtual machine(s) on a host machine. As a developer you can, on your local machine, what ever OS you are using, start up a isolated virtual machine running a different OS. This is often done by installing a [hypervisor](https://en.wikipedia.org/wiki/Hypervisor) which is a program that lays.

Virtualization is also very important when talking cloud computing and IT architecture. Virtualization of machines give opportunities to easy add, change and remove servers in a cloud solution. This is important i modern web scale solution where the applications/solutions have to scale in a fast and easy way without the need of buying new hardware.

If you want to learn more about different virtualization techniques [here is an article for you](http://www.virtuatopia.com/index.php/An_Overview_of_Virtualization_Techniques)


## So what is a container?
Just as we define the virtualized machine as an isolated operating system on a host system, the same goes for containers. We can describe it further as self-contained execution environments. Containers have their own isolated CPU, memory, I/O and network resources, but share the kernel of the host operating system. The difference from virtual machines is that containers are more light weight, faster to start and handling in different scenarios. This make containers a good fit when working with web application solutions, especially in a situation where scale is important. Hopefully you can also see the connection to developing [microservices](https://github.com/CS-LNU-Learning-Objects/web-application-architecture/blob/master/microservices.md) where containers is ideal for handling different microservices.

In this text we will concentrate on Linux containers and especially Docker. Containers is nothing new and you can find other similar techniques like FreeBSD Jails and Solaris Zones The Linux systems have features like [cgroups](https://en.wikipedia.org/wiki/Cgroups) and [namespaces](http://man7.org/linux/man-pages/man7/namespaces.7.html) that helps with the isolation and handling of system resources so that they get dedicated to specific processes.

To better understand the difference between virtual machines and containers the following image can be used. The Docker engine is the one thing handling the different containers and make sure the containers can use the shared kernel.

![conatiners](https://github.com/CS-LNU-Learning-Objects/web-application-architecture/raw/master/images/dockervsvirt.jpg)

_Image form docker.com_

The original Linux Container is Linux Containers, known as LXC. This is a system operating system-level virtualization method running multiple isolated Linux systems on a single host with the help of namespaces and cgroups. The Linux containers helped the system to separate the operating system-level work from the applications running, leaving a clean and minimal OS.

### Docker
In the beginning [Docker](https://docker.com) used Linux containers and introduced several significant changes to LXC to get more portable and flexible containers. They aimed to get a way to deploy, replicate, move and backup environments more quickly and easily then the more common virtual machines. In short word, they tried to bring a more cloud-like flexibility to any infrastructure. The Docker project evolved and started to developed its own container runtime environment instead of build specialized LXC. It has became a very popular utility to efficiently create, ship and run containers.

### Docker - Containers for developers
As a developer you already heard about Docker somewhere and you will probably hear a lot more the following years. There are some points that are especially interesting when discussing Docker vs. LCX and that is  the way Docker has been popular in the DevOps community.

As said above, we can see that Docker make use of low-level technologies and makes it simple to use through a powerful ecosystem built around the technologies.

### The Docker architecture

Docker is using a server-client architecture, meaning that when installing Docker we will have a client cli where we execute commands. These commands is delegated to the Docker daemon which is the server part. It is here all the magic takes place, here containers are build and managed. The client use an REST API to communicate with the server daemon. The API and the daemon is often called *Docker Engine*

![Docker architecture](https://docs.docker.com/engine/article-img/architecture.svg)

_Image taken from docker.com_

Often is the client and the daemon running on the same host machine but that is not necessary. When using docker we also talk about a registry where we can get images for creating a container. A image is a read-only template on how to build a container. For example a image can contain a Ubuntu with Node.js and a web application installed.

You store your images in a registry (private or public). This also means that you can get others predefined images from a public registry. Check up [the Docker hub](https://hub.docker.com/) for more information.

If the docker daemon gets a command from the client to get a specific image it will check for it in the registry loading it into the docker engine and produce a container. This container should hold everything the application/microservice needs as an secure and isolated unit. This container can be start, stopped, moved and deleted.

More information will be found in the [docker documentation](https://docs.docker.com/engine/understanding-docker/)

### Characteristics

So why do we think Docker is so popular? Of course we understand the simplicity and lightweight way of handling containers. The Docker team has also taken powerful technologies used in the LXC and make it more simple for developers. Some key points follow bellow.

* **Layers**
  One of the things that make the handling of docker images lightweight is that Docker is using a layered file system, [UnionFS](https://en.wikipedia.org/wiki/UnionFS). This means that if we will make a change of an original image a new layer is created instead of recreate the whole image. If you didn't have UnionFS, an 200MB image run 5 times as 5 separates containers would mean 1GB of disk space. This also means that a change can be rolled back by removing the layer.


* **Single process**

  Docker tries to restricts containers to run as a single process. Imagine that you setting up a dynamic web application. You will need to have a web server, a reversed proxy, some kind of database server, some persistent storage, maybe some caching server and so on. Best practice is to create a own container for each of this process. Maybe a node.js-container running the web application, a nginx-container as an reversed proxy, a mongodb-container for database and one container for persistent storage. If you have web scale in mind each service have multiple containers.

  This will get you a more granular update process. No need to interfere with the web server if a database update is done. Also, this is ideal for building microservices-based applications.

* **Stateless, read-only**

  Docker containers are designed to be stateless. Docker does not support persistent storage but have the ability to mount host storage through "Docker volumes" outside the container itself.

* **Portable**

  Docker abstracts away networking, storage and OS details from the application. The application/microservice is independent form low level configurations and resources. Therefore you can move your container to other docker environment. That is very convenient in a continuous development workflow when shifting containers from different servers in the pipeline. This is probably why docker is a common used platform in DevOps communities.

  The nature of Docker (and containers) that we can decouple applications from the underlying OS. This enables portability and cloud-like flexibility for developers on an other level then with virtualization. Also remember that container/docker is a developer-driven era. Gone are the problems with applications working on the developer server but not on the production server. Since containers isolate the application and share the underlying resources



### Tools in the Docker ecosystem
When you start reading about Docker you will step into some of the tools that the Docker platform includes. The two listed below is beyond the scope of this text but feel free to explore the tools by yourself.

* [Compose](https://github.com/docker/compose) is a tool for defining and running complex applications with Docker. With compose, you define a multi-container application in a single file, then spin your application up in a single command which does everything that needs to be done to get it running.

* [Swarm](https://github.com/docker/swarm) is a native clustering tool for Docker. Swarm pools together several Docker hosts and exposes them as a single virtual Docker host. It serves the standard Docker API, so any tool that already works with Docker can now transparently scale up to multiple hosts.

### Getting started with Docker
This text will not teach you the practical steps of using Docker. You will have to read the documentation for this. But here is a very simple example of starting a simple Nginx container (Nginx is a popular web server).

First of all you have to [install docker for your OS](https://docs.docker.com/engine/installation/). Maybe you don´t want to put it on your local OS and of course you can install it on a virtualized machine, through Virtual Box or some other hypervisor.

#### The dockerfile
When creating a container you often define its content in a dockerfile. This file allows us to give instructions to the Docker engine which base image to use and what commands to give it. Look at the example below taken from https://github.com/dockerfile/nginx:

```
# Pull base image.
FROM dockerfile/ubuntu

# Install Nginx.
RUN \
  add-apt-repository -y ppa:nginx/stable && \
  apt-get update && \
  apt-get install -y nginx && \
  rm -rf /var/lib/apt/lists/* && \
  echo "\ndaemon off;" >> /etc/nginx/nginx.conf && \
  chown -R www-data:www-data /var/lib/nginx

# Define mountable directories.
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www/html"]


# Define default command.
CMD ["nginx"]

# Expose ports.
EXPOSE 80
EXPOSE 443

```

Here follow a fast explanation over the commands:

FROM is telling Docker from which base image the container should be created. In this case it will be from a ubuntu image.

RUN will run a couple of commands on the Ubuntu machine. In this case it will install the latest stable Nginx version and doing some other linux commands to configure it. The endings of && \ gives us opportunity to run all that we want without making several RUN commands. This is the preferable way since making a RUN statement before each row will produce a separate image for each statement.


VOLUME is mounting different directories. As you probably remember does not docker have any way of handling storage other than mounting volumes to the container. In this case it mounts important "nginx-directories" from the container to the host system.

CMD defines a command that will run when the container starts.

EXPOSE exposes the standard HTTP ports so that we browse to the web server.

### Get predefined images
Pretty soon you will realize that the [Docker Hub](https://hub.docker.com/) is a gold mine when getting god images for Docker containers. Docker is an open community and if you search on the hub (or on github) you will find many people defining different services you can use. Try find a Apache with PHP for example. I bet you find one and could have a Linux server with Apache and PHP running in a couple of minutes. It is also a very good way to learn writing own docker-files and linking them together.

### Start learning about docker
This text will not go through the practical view of Docker more than this. The best way to start learning about Docker and creating your own containers is to visit the [docker homepage and study the documentation](https://docs.docker.com/).

## References and further reading
[101 Containers](http://www.developer.com/design/containers-101.html)

[Linux containers and Docker explained](http://www.infoworld.com/article/3072929/linux/containers-101-linux-containers-and-docker-explained.html)

Of course is the docker documentation a gold mine for starting using docker.
A good start - https://docs.docker.com/engine/understanding-docker/
