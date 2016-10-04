# Windows

You have two options for installing Docker on Windows:

* [Docker for Windows](https://docs.docker.com/engine/installation/windows/#docker-for-windows)
* [Docker Toolbox](https://docs.docker.com/engine/installation/windows/#docker-toolbox)

你有两个选项将Docker安装在Windows上：

* [Docker for Windows](https://docs.docker.com/engine/installation/windows/#docker-for-windows)
* [Docker Toolbox](https://docs.docker.com/engine/installation/windows/#docker-toolbox)

## Docker for Windows

Docker for Windows is our newest offering for PCs. It runs as a native Windows application and uses Hyper-V to virtualize the Docker Engine environment and Linux kernel-specific features for the Docker daemon.

Docker for Windows 是我们最新提供给Windows的产品。他像原生Windows程序那样运行并且使用Hyper-V去虚拟Docker引擎环境和Linux内核功能给Docker守护进程。

Go to [Getting Started with Docker for Windows](https://docs.docker.com/docker-for-windows/) for download and install instructions, and to learn all about Docker for Windows.

去[Getting Started with Docker for Windows](https://docs.docker.com/docker-for-windows/)页面下载和查看指南，并且学习所有关于Docker for Windows的内容。

**Requirements**

* 64bit Windows 10 Pro, Enterprise and Education \(1511 November update, Build 10586 or later\). In the future we will support more versions of Windows 10.

* The Hyper-V package must be enabled. The Docker for Windows installer will enable it for you, if needed. \(This requires a reboot\).


**需求**

* 64位Windows 10旗舰版，企业版和教育版。我们会支持Windows 10更多的功能。

## Docker Toolbox

If you have an earlier Windows system that doesn’t meet the Docker for Windows requirements, [get Docker Toolbox](https://www.docker.com/products/docker-toolbox).

如果你使用更早的Windows系统不符合Docker for Windows的需求，使用[Docker Toolbox 。](https://www.docker.com/products/docker-toolbox)

See [Docker Toolbox Overview](https://docs.docker.com/toolbox/overview/) for help on installing Docker with Toolbox.

点击[Docker Toolbox Overview](https://docs.docker.com/toolbox/overview/)查看Docker Toolbox安装帮助。

The Docker Toolbox setup does not run Docker natively on Windows. Instead, it uses `docker-machine` to create and attach to a virtual machine \(VM\). This machine is a Linux VM that hosts Docker for you on your Windows system.

Docker Toolbox并没有原生的运行在Windows。相反，它使用`docker-machine`创建一个虚拟机。这个机器是一个运行着Docker的linux虚拟机。

**Requirements**

**需求**

To run Docker, your machine must have a 64-bit operating system running Windows 7 or higher. Additionally, you must make sure that virtualization is enabled on your machine. For details, see the [Toolbox install instructions for Windows](https://docs.docker.com/toolbox/toolbox_install_windows/).

要运行Docker，你的机器至少需要运行64位Windows 7或更高版本。另外你必须确保你的机器支持虚拟化。更多细节，查看[Toolbox install instructions for Windows](https://docs.docker.com/toolbox/toolbox_install_windows/)。

## Learning more

## 学习更多

* If you are new to Docker, try out the [Getting Started](https://docs.docker.com/engine/getstarted/) tutorial for a hands-on tour, including using Docker commands, running containers, building images, and working with Docker Hub.

* You can find more extensive examples in [Learn by example](https://docs.docker.com/engine/tutorials/) and in the [Docker Engine User Guide](https://docs.docker.com/engine/userguide/).

* If you are interested in using the Kitematic GUI, see the [Kitematic user guide](https://docs.docker.com/kitematic/userguide/).

* 如果你是Docker新手，尝试使用[Getting Started](https://docs.docker.com/engine/getstarted/)教程的动手之旅，这包括使用Docker命令行，运行容器，构建镜像和与 Docker Hub一起工作。

* 你可以在 [Learn by example ](https://docs.docker.com/engine/tutorials/)和 [Docker Engine User Guide](https://docs.docker.com/engine/userguide/) 找到更多的例子。

* 如果你有兴趣使用 Kitematic 图形界面, 查看 [Kitematic user guide](https://docs.docker.com/kitematic/userguide/)。


> **Note**: The Boot2Docker command line was deprecated several releases &gt; back in favor of Docker Machine, and now Docker for Windows.
> 
> 注意：Boot2Docker命令行已经在多个版本之前被废弃，现在已经被Docker for Windows废弃。

