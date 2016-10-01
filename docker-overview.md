# Docker 概述

Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

Docker是一个为开发，托管，运行应用的开源的平台。Docker允许你从你的基础设施上拆分你的应用，因此你可以进行快速迭代。通过Docker，你可以像管理你的应用那样管理你的基础设施。得益于Docker可以快速的进行托管，测试和部署，你可以显著的节省从编写代码到发布产品所需的时间。

## What is the Docker platform?

## 什么是Docker平台？

Docker provides the ability to package and run an application in a loosely isolated environment called a container. The isolation and security allow you to run many containers simultaneously on a given host. Because of the lightweight nature of containers, which run without the extra load of a hypervisor, you can run more containers on a given hardware combination than if you were using virtual machines.

Docker provides tooling and a platform to manage the lifecycle of your containers:

* Encapsulate your applications \(and supporting components\) into Docker containers
* Distribute and ship those containers to your teams for further development and testing
* Deploy those applications to your production environment, whether it is in a local data center or the Cloud

Docker允许你在一个轻量隔离的容器中打包和运行应用。隔离和安全允许你在同一台机器上运行多个容器。由于容器天生的轻量级，相比虚拟机运行时不需要加载更多的东西，所以你可以在相同的硬件条件下运行更多的数量。

Docker为你应用的整个生命周期提供工具和平台：

* 你的应用（包含依赖）打包进容器。
* 为了未来的开发和测试分发和托管这些容器给你的团队。
* 部署这些应用到你的生产环境，无论它是本地的数据中心还是在云端。

## What is Docker Engine?

## 什么是Docker引擎？

_Docker Engine_ is a client-server application with these major components:

* A server which is a type of long-running program called a daemon process.

* A REST API which specifies interfaces that programs can use to talk to the daemon and instruct it what to do.

* A command line interface \(CLI\) client.


Docker引擎是一个包含以下几个重要组成部分的client-server应用：

* server：一个叫做守护进程的长时间运行的程序。
* REST API：和守护进程通信并告诉它该做什么的具体接口。
* client： 命令行（CLI）

![](/assets/engine-components-flow.png)
The CLI uses the Docker REST API to control or interact with the Docker daemon through scripting or direct CLI commands. Many other Docker applications use the underlying API and CLI.

The daemon creates and manages Docker _objects_, such as images, containers, networks, and data volumes.

CLI通过Docker REST API使用脚本或者直接的CLI命令控制器Docker守护进程。许多其他的Docker应用使用底层的API和CLI。

守护进程创建和管理Docker对象，比如镜像，容器，网络，和数据卷。

> **Note:** Docker is licensed under the open source Apache 2.0 license.
> 
> 注意：Docker在开源 Apache 2.0 授权之下

## What can I use Docker for?

## 我可以用Docker做什么？

_Fast, consistent delivery of your applications_

Docker can streamline the development lifecycle by allowing developers to work in standardized environments using local containers which provide your applications and services. You can also integrate Docker into your continuous integration and continuous deployment \(CI\/CD\) workflow.

Consider the following example scenario. Your developers write code locally and share their work with their colleagues using Docker containers. They can use Docker to push their applications into a test environment and execute automated and manual tests. When developers find problems, they can fix them in the development environment and redeploy them to the test environment for testing. When testing is complete, getting the fix to the customer is as simple as pushing the updated image to the production environment.

_快速，一致的分发你的应用_

开发者通过使用标准统一的本地化Docker容器使开发工作流程化。你可以将Docker统一到你的持续集成和持续开发工作流程中。

想象一下以下示例情景。你的开发人员通过容器向他的同事分享他的工作成果。他们可以把她们的应用推送到测试环境进行自动化测试。当开发者发现问题，然后他们在开发环境修复这些问题并重新部署到测试环境进行测试。当测试通过，推送到客户那里就仅仅是简单的推送到生产环境。

_Responsive deployment and scaling_

Docker’s container-based platform allows for highly portable workloads. Docker containers can run on a developer’s local host, on physical or virtual machines in a data center, in the Cloud, or in a mixture of environments.

Docker’s portability and lightweight nature also make it easy to dynamically manage workloads, scaling up or tearing down applications and services as business needs dictate, in near real time.

_响应式部署和扩大_

Docker基于容器的平台允许高可移植工作量。Docker容器可以运行在开发者自己的本地机器上，在物理或虚拟的数据中心，在云端，或者在混合环境中。

为了业务需求，Docker的可移植性和天然的轻量可以很方便快速的动态管理负载，扩大或拆除业务。

_Running more workloads on the same hardware_

Docker is lightweight and fast. It provides a viable, cost-effective alternative to hypervisor-based virtual machines, allowing you to use more of your compute capacity to achieve your business goals. This is useful in high density environments and for small and medium deployments where you need to do more with fewer resources.

_在相同的硬件上完成更多的工作量_

Docker是轻量高效的。它提供一个可行的，花费少的虚拟机替代品，允许你使用你的电脑实现更多的商业价值。这对于在更少的资源上运行更多的中小型应用非常有用。

## What is Docker’s architecture?

## 什么是Docker的构筑哲学？

Docker uses a client-server architecture. The Docker _client_ talks to the Docker _daemon_, which does the heavy lifting of building, running, and distributing your Docker containers. The Docker client and daemon _can_ run on the same system, or you can connect a Docker client to a remote Docker daemon. The Docker client and daemon communicate via sockets or through a REST API.

Docker 使用client-server的构建方式。_client_和_Docker_守护进程进行通讯，来进行构建，运行，和支配你的Docker容器。Docker的client和守护进程可以运行在相同的系统上，或者你可以Docker client连接远程的Docker守护进程。Docker client通过REST API 使用sockets和守护进程进行通讯。

![](/assets/architecture.svg)

### The Docker daemon

### Docker 守护进程

The Docker daemon runs on a host machine. The user uses the Docker client to interact with the daemon.

Docekr守护进程运行在主机上。用户通过Docker client和守护进程通讯。

### The Docker client

### Docker 客户端

The Docker client, in the form of the `docker` binary, is the primary user interface to Docker. It accepts commands and configuration flags from the user and communicates with a Docker daemon. One client can even communicate with multiple unrelated daemons.

Docker client是`docker`的组成部分之一，是Docker主要的用户界面。主要接受从用户发出的命令和配置标识来和Docker守护进程通讯。一个client可以和多个不相关的守护进程通讯。

### Inside Docker

### 走进Docker

To understand Docker’s internals, you need to know about _images_, _registries_, and _containers_.

要了解Docker的里面，你需要知道镜像，仓库，和容器。

#### Docker images

#### Docker 镜像

A Docker _image_ is a read-only template with instructions for creating a Docker container. For example, an image might contain an Ubuntu operating system with Apache web server and your web application installed. You can build or update images from scratch or download and use images created by others. An image may be based on, or may extend, one or more other images. A docker image is described in text file called a _Dockerfile_, which has a simple, well-defined syntax. For more details about images, see [How does a Docker image work?](https://docs.docker.com/engine/understanding-docker/#how-does-a-docker-image-work).

Docker images are the **build** component of Docker.

Docker镜像就是创建容器的只读模板。举个栗子，一个包含Ubuntu系统，Apache，和你的web应用的镜像。你可以通过下载或拼凑创建或更新容器，你也可以使用别人创建的镜像。一个镜像可能基于或者扩展一个或其他几个镜像。每个docker镜像通过简单并具有完整规则的_Dockerfile_来描述。更多关于镜像的信息，查看[ Docker镜像是怎么工作的？](#how-does-a-docker-image-work)

#### Docker containers

#### Docker 容器

A Docker container is a runnable instance of a Docker image. You can run, start, stop, move, or delete a container using Docker API or CLI commands. When you run a container, you can provide configuration metadata such as networking information or environment variables. Each container is an isolated and secure application platform, but can be given access to resources running in a different host or container, as well as persistent storage or databases. For more details about containers, see [How does a container work?](https://docs.docker.com/engine/understanding-docker/#how-does-a-container-work).

Docker containers are the **run** component of Docker.

Docker容器是Docker镜像的一个运行实例。你可以使用Docker的API或CLI命令行运行，开始，停止，移动或删除容器。当你运行一个容器，你可以提供配置元数据比如网络信息或环境变量。每一个容器就是一个独立和安全的应用平台，但是它可以使资源运行在不同的主机或容器，比如独立的存储或数据库。更多关于容器的介绍，查看：[容器是怎么工作的？](#how-does-a-container-work)

#### Docker registries

#### Docker 仓库

A docker registry is a library of images. A registry can be public or private, and can be on the same server as the Docker daemon or Docker client, or on a totally separate server. For more details about registries, see [How does a Docker registry work?](https://docs.docker.com/engine/understanding-docker/#how-does-a-docker-registry-work)

Docker registries are the **distribution** component of Docker.

一个Docker仓库就是镜像的图书馆。一个仓库既可以是公开的也可以是私有的，并且可以作为Docker守护进程或Docker客户端在同一服务器或独立的服务器上。更多关于仓库的细节，查看 [Docker是怎么工作的？](#how-does-a-docker-registry-work)

#### Docker services

#### Docker 服务

A Docker _service_ allows a _swarm_ of Docker nodes to work together, running a defined number of instances of a replica task, which is itself a Docker image. You can specify the number of concurrent replica tasks to run, and the swarm manager ensures that the load is spread evenly across the worker nodes. To the consumer, the Docker service appears to be a single application. Docker Engine supports swarm mode in Docker 1.12 and higher.

Docker services are the **scalability** component of Docker.

Docker服务支持多个Docker节点协同的集群工作，运行一个定义的副本任务，它们本身就是一个Docker镜像。你可以指定同时运行任务的数量，并且集群管理确保压力被分散到各个工作节点。对于顾客，Docker服务显示为单个应用。Docker引擎支持集群在Docker1.12或更高的版本。

Docker服务的可扩展性是Docker的重要性能之一。

### How does a Docker image work?

### Docker镜像是怎么工作的?

Docker images are read-only templates from which Docker containers are instantiated. Each image consists of a series of layers. Docker uses [union file systems](http://en.wikipedia.org/wiki/UnionFS) to combine these layers into a single image. Union file systems allow files and directories of separate file systems, known as branches, to be transparently overlaid, forming a single coherent file system.

Docker镜像是从Docker容器中实例化的只读模板。每个镜像由一系列的层组成。Docker使用联合文件系统把这些层组成单个镜像。联合文件系统可以使像分支这样的属于独立文件系统的文件和目录叠加形成一个独立一致的文件系统。

These layers are one of the reasons Docker is so lightweight. When you change a Docker image, such as when you update an application to a new version, a new layer is built and replaces only the layer it updates. The other layers remain intact. To distribute the update, you only need to transfer the updated layer. Layering speeds up distribution of Docker images. Docker determines which layers need to be updated at runtime.

这些层是Docker如此轻量的原因之一。当你改变了你的Docker镜像，比如当你更新你的应用到一个新的版本，Docker仅仅新构建一个层去替换需要更新的层。其他的层保持不变。要分发这个更新，你只需要传输更新过的层就可以了。分层加速了Docker镜像的分发。Docker在运行时很明确的知道哪些层需要更新。

An image is defined in a Dockerfile. Every image starts from a base image, such as `ubuntu`, a base Ubuntu image, or `fedora`, a base Fedora image. You can also use images of your own as the basis for a new image, for example if you have a base Apache image you could use this as the base of all your web application images. The base image is defined using the `FROM` keyword in the dockerfile.

一个镜像通个Dockerfile来定义。每一个镜像开始于基础镜像，比如 `ubuntu`一个基于Ubuntu的镜像，或者是`fedora`一个基于Fedora的镜像。你也可以使用你自己的基础组件作为新的镜像，比如你有一个基于Apache的镜像，你可以使用它作为你所有web应用的基础镜像。基础镜像使用`FROM`关键词在dockerfile中定义

> **Note:** [Docker Hub](https://hub.docker.com/) is a public registry and stores images.
> 
> 注意：[Docker Hub](https://hub.docker.com/) 是一个存储镜像的公共仓库。

The docker image is built from the base image using a simple, descriptive set of steps we call _instructions_, which are stored in a `Dockerfile`. Each instruction creates a new layer in the image. Some examples of Dockerfile instructions are:

* Specify the base image \(`FROM`\)
* Specify the maintainer \(`MAINTAINER`\)
* Run a command \(`RUN`\)
* Add a file or directory \(`ADD`\)
* Create an environment variable \(`ENV`\)
* What process to run when launching a container from this image \(`CMD`\)

Docker镜像通过存储在Dockerfile中一系列简单，我们称之为指令的描述性设定构建。每一条指令在镜像中创建一个新的层。一些Dockerfile指令比如：
* 指定基础镜像\(`FROM`\)
* 指定维护\(`MAINTAINER`\)
* 运行一个命令\(`RUN`\)
* 添加一个文件或目录\(`ADD`\)
* 创建一个环境变量\(`ENV`\)
* 当从这个镜像中运行一个容器时运行哪个进程 \(`CMD`\)

Docker reads this `Dockerfile` when you request a build of an image, executes the instructions, and returns the image.

Docker读取`Dockerfile` 当你请求构建一个镜像，执行指令，返回镜像。

### How does a Docker registry work?

### Docker仓库是怎么工作的?

A Docker registry stores Docker images. After you build a Docker image, you can _push_ it to a public registry such as[Docker Hub](https://hub.docker.com/) or to a private registry running behind your firewall. You can also search for existing images and pull them from the registry to a host.

[Docker Hub](http://hub.docker.com/) is a public Docker registry which serves a huge collection of existing images and allows you to contribute your own. For more information, go to [Docker Registry](https://docs.docker.com/registry/overview/) and [Docker Trusted Registry](https://docs.docker.com/docker-trusted-registry/overview/).

[Docker store](http://store.docker.com/) allows you to buy and sell Docker images. For image, you can buy a Docker image containing an application or service from the software vendor, and use the image to deploy the application into your testing, staging, and production environments, and upgrade the application by pulling the new version of the image and redeploying the containers. Docker Store is currently in private beta.

### How does a container work?

### 容器是怎么工作的?

A container uses the host machine’s Linux kernel, and consists of any extra files you add when the image is created, along with metadata associated with the container at creation or when the container is started. Each container is built from an image. The image defines the container’s contents, which process to run when the container is launched, and a variety of other configuration details. The Docker image is read-only. When Docker runs a container from an image, it adds a read-write layer on top of the image \(using a UnionFS as we saw earlier\) in which your application runs.

#### What happens when you run a container?

#### 当你运行容器时发生了什么?

When you use the `docker run` CLI command or the equivalent API, the Docker Engine client instructs the Docker daemon to run a container. This example tells the Docker daemon to run a container using the `ubuntu` Docker image, to remain in the foreground in interactive mode \(`-i`\), and to run the `/bin/bash` command.

```
$ docker run -i -t ubuntu /bin/bash

```

When you run this command, Docker Engine does the following:

1. **Pulls the **`ubuntu`** image:** Docker Engine checks for the presence of the `ubuntu` image. If the image already exists locally, Docker Engine uses it for the new container. Otherwise, then Docker Engine pulls it from [Docker Hub](https://hub.docker.com/).

2. **Creates a new container:** Docker uses the image to create a container.

3. **Allocates a filesystem and mounts a read-write \*\***_layer_**\*\*:** The container is created in the file system and a read-write layer is added to the image.

4. **Allocates a network \/ bridge interface:** Creates a network interface that allows the Docker container to talk to the local host.

5. **Sets up an IP address:** Finds and attaches an available IP address from a pool.

6. **Executes a process that you specify:** Executes the `/bin/bash` executable.

7. **Captures and provides application output:** Connects and logs standard input, outputs and errors for you to see how your application is running, because you requested interactive mode.


Your container is now running. You can manage and interact with it, use the services and applications it provides, and eventually stop and remove it.

## The underlying technology

## 底层技术

Docker is written in [Go](https://golang.org/) and takes advantage of several features of the Linux kernel to deliver its functionality.

### Namespaces

### 命名空间

Docker uses a technology called `namespaces` to provide the isolated workspace called the _container_. When you run a container, Docker creates a set of _namespaces_ for that container.

These namespaces provide a layer of isolation. Each aspect of a container runs in a separate namespace and its access is limited to that namespace.

Docker Engine uses namespaces such as the following on Linux:

* **The **`pid`** namespace:** Process isolation \(PID: Process ID\).
* **The **`net`** namespace:** Managing network interfaces \(NET: Networking\).
* **The **`ipc`** namespace:** Managing access to IPC resources \(IPC: InterProcess Communication\).
* **The **`mnt`** namespace:** Managing filesystem mount points \(MNT: Mount\).
* **The **`uts`** namespace:** Isolating kernel and version identifiers. \(UTS: Unix Timesharing System\).

### Control groups

### 控制集合

Docker Engine on Linux also relies on another technology called _control groups_ \(`cgroups`\). A cgroup limits an application to a specific set of resources. Control groups allow Docker Engine to share available hardware resources to containers and optionally enforce limits and constraints. For example, you can limit the memory available to a specific container.

### Union file systems

### 联合文件系统

Union file systems, or UnionFS, are file systems that operate by creating layers, making them very lightweight and fast. Docker Engine uses UnionFS to provide the building blocks for containers. Docker Engine can use multiple UnionFS variants, including AUFS, btrfs, vfs, and DeviceMapper.

### Container format

### 容器格式化

Docker Engine combines the namespaces, control groups, and UnionFS into a wrapper called a container format. The default container format is `libcontainer`. In the future, Docker may support other container formats by integrating with technologies such as BSD Jails or Solaris Zones.

