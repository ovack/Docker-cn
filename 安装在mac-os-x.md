# Mac OS X

You have two options for installing Docker on Mac:

* [Docker for Mac](https://docs.docker.com/engine/installation/mac/#docker-for-mac)
* [Docker Toolbox](https://docs.docker.com/engine/installation/mac/#docker-toolbox)

在Mac上安装Docker你有两个选项：

* [Docker for Mac](https://docs.docker.com/engine/installation/mac/#docker-for-mac)
* [Docker Toolbox](https://docs.docker.com/engine/installation/mac/#docker-toolbox)

## **Docker for Mac**

Docker for Mac is our newest offering for the Mac. It runs as a native Mac application and uses [xhyve](https://github.com/mist64/xhyve/) to virtualize the Docker Engine environment and Linux kernel-specific features for the Docker daemon.

Docker for Mac 是我们最新提供给Mac的。他想原生Mac程序那样运行并且使用[xhyve](https://github.com/mist64/xhyve/)去虚拟Docker引擎环境和Linux内核功能给Docker守护进程。

Go to [Getting Started with Docker for Mac](https://docs.docker.com/docker-for-mac/) for download and install instructions, and to learn all about Docker for Mac.

去[Getting Started with Docker for Mac](https://docs.docker.com/docker-for-mac/) 页面下载和查看指南，并且学习所有关于Docker的内容。

**Requirements**

* Mac must be a 2010 or newer model, with Intel’s hardware support for memory management unit \(MMU\) virtualization; i.e., Extended Page Tables \(EPT\)

* OS X 10.10.3 Yosemite or newer

* At least 4GB of RAM

* VirtualBox prior to version 4.3.30 must NOT be installed \(it is incompatible with Docker for Mac\). Docker for Mac will error out on install in this case. Uninstall the older version of VirtualBox and re-try the install.


**需求**

* 2010年或更新的Mac，支持虚拟内存管理的Intel硬件；也就是扩展页表。
* OS X 10.10.3 Yosemite或更新的系统。

* 至少4G内存。

* 不能安装4.3.30之前版本的VirtualBox（和Docker for Mac不兼容）。Docker for Mac 会在安装之前版本VirtualBox的机器上出错。写在老版本的VirtualBox然后重新安装Docker for Mac。


## Docker Toolbox

If you have an earlier Mac that doesn’t meet the Docker for Mac requirements, [get Docker Toolbox](https://www.docker.com/products/docker-toolbox) for the Mac.

如果你使用比要求更老的Mac机器，则使用 [get Docker Toolbox。](https://www.docker.com/products/docker-toolbox)

See [Docker Toolbox Overview](https://docs.docker.com/toolbox/overview/) for help on installing Docker with Toolbox.

点击[Docker Toolbox Overview](https://docs.docker.com/toolbox/overview/)查看Docker Toolbox安装教程。

The Docker Toolbox setup does not run Docker natively in OS X. Instead, it uses `docker-machine` to create and attach to a virtual machine \(VM\). This machine is a Linux VM that hosts Docker for you on your Mac.

Docker Toolbox并没有原生的运行在OS X。相反，它使用`docker-machine`创建一个虚拟机。这个机器是一个运行着Docker的linux虚拟机。

**Requirements**

Your Mac must be running OS X 10.8 “Mountain Lion” or newer to install the Docker Toolbox. Full install instructions are at [Toolbox install instructions for Mac](https://docs.docker.com/toolbox/toolbox_install_mac/).

**需求**

你的Mac必须运行OS X 10.8或最新的版本才能安装Docker Toolbox。安装过程详见[Toolbox install instructions for Mac。](https://docs.docker.com/toolbox/toolbox_install_mac/)

## Learning more

## 学习更多

* If you are new to Docker, try out the [Getting Started](https://docs.docker.com/engine/getstarted/) tutorial for a hands-on tour, including using Docker commands, running containers, building images, and working with Docker Hub.

* You can find more extensive examples in [Learn by example](https://docs.docker.com/engine/tutorials/) and in the [Docker Engine User Guide](https://docs.docker.com/engine/userguide/).

* If you are interested in using the Kitematic GUI, see the [Kitematic user guide](https://docs.docker.com/kitematic/userguide/).

* 如果你是Docker新手，尝试使用[Getting Started](https://docs.docker.com/engine/getstarted/)教程的动手之旅，这包括使用Docker命令行，运行容器，构建镜像和与 Docker Hub一起工作。
* 你可以在 [Learn by example ](https://docs.docker.com/engine/tutorials/)和 [Docker Engine User Guide](https://docs.docker.com/engine/userguide/) 找到更多的例子。
* 如果你有兴趣使用 Kitematic 图形界面, 查看 [Kitematic user guide](https://docs.docker.com/kitematic/userguide/)。

> **Note**: The Boot2Docker command line was deprecated several releases back in favor of Docker Machine, and now Docker for Mac.
> 
> 注意：Boot2Docker命令行已经在多个版本之前被废弃，现在已经被Docker for Mac废弃。

