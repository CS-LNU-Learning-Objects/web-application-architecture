This text is written to give a short introduction to containers and docker in particular. It´s mainly written from a developers point of view.

# Introduction to containers and Docker
To understand what a container is you first have to be familiar with what virtualization is. That is a technique that allows you to run independent virtual machine on a host machine. As a developer you can on your local machine, what ever OS you are using, start up a isolated virtual machine running a different OS. This is often done by installing a [hypervisor](https://en.wikipedia.org/wiki/Hypervisor) which is a program that lays.


Virtualization is also very important when talking cloud computing and IT architecture. Virtualization of machines give opportunities to easy add, change and remove servers in a cloud solution. This is important i modern web scale solution where the applications/solutions have to scale in a fast and easy way without the need of buying new hardware.

If you want to learn more about different virtualization techniques [here is an article for you](http://www.virtuatopia.com/index.php/An_Overview_of_Virtualization_Techniques)



## So what is a container
Just as we define the virtualized machine as an isolated operating system on a host system the same goes for containers. We can describe it further as self-contained execution environments. They have their own isolated CPU, memory, I/O and network resources, but share the kernel of the host operating system. The difference from virtual machines is often  that it comes without all the weight and startup overhead of the guest operating system. This make containers a good fit when working with web application solutions, especially in a situation where scale is important.

In this text we will concentrate on Linux containers and especially docker. Containers is nothing new and you can find other reminding techniques like FreeBSD Jails and Solaris Zones The Linux systems have features like [cgroups](https://en.wikipedia.org/wiki/Cgroups) and [namespaces](http://man7.org/linux/man-pages/man7/namespaces.7.html) that helps with the isolation and handling of system resources so that they get dedicated to specific processes.

To get a view over the difference between virtual machines and containers the following image can be used. In this movie the Docker engine is the one thing handling the different containers and make sure the containers can use the shared kernel.

![conatiners](./images/dockervsvirt.jpg)

_Image form docker.com_

The orginal Linux Container is Linux Containers, known as LXC. This is a system operating system-level virtualization method running multiple isolated Linux systems on a single host with the help of namespaces and cgroups. The Linux containers helped the system to separate the operating system-level work from the applications running leaving a clean an minimal OS.

### Docker
In the beginning [Docker](https://docker.com) used Linux containers and introduced several significant changes to LXC to get more portable and flexible containers. They aimed to get a way to deploy, replicate, move and back up environments more quickly and easily then the more common virtual machines. In short word, they tried to bring a more cloud-like flexibility to any infrastructure. The project started to evolve and started to developed its own container runtime environment instead of build specialized LXC. It became a very popular utility to effciently create, ship and run containers.

### Docker for web development
