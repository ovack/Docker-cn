# Fedora[](https://docs.docker.com/engine/installation/linux/fedora/#fedora)

Docker支持Fedora 22，23，和24版本。这篇指南使用Docker管理的安装包和安装工具，确保你获取的是最新版本的Docker。如果你希望使用Fedora-managed安装包，查阅你的Fedora发行版文档。

## Prerequisites[](https://docs.docker.com/engine/installation/linux/fedora/#prerequisites)

Docker需要64位操作系统和3.10以上的linux内核。

检查你的内核版本，打开一个终端和使用`uname -r`命令来打印你的内核版本：

```bash
$ uname -r
3.19.5-100.fc21.x86_64
```

如果你使用老的内核版本，你必须更新它。

最后，我们推荐你完全更新你的系统。请记住，您的系统应该完全修补，已修复任何明确的内核错误。任何已报告的内核bug可能在最近的linux内核包中被修复。

## Install Docker Engine[](https://docs.docker.com/engine/installation/linux/fedora/#install-docker-engine)

这里有两种方式安装Docker引擎，你可以 [install using the `dnf` package manager](https://docs.docker.com/engine/installation/linux/fedora/#install-with-dnf)。或者你可以使用`curl`[with the `get.docker.com` site](https://docs.docker.com/engine/installation/linux/fedora/#install-with-the-script)。第二种方式运行一个安装脚本也是通过 `dnf`包管理安装。

### Install with DNF[](https://docs.docker.com/engine/installation/linux/fedora/#install-with-dnf)

1. 使用具有 `sudo` 或  `root` 权限的用户登录你的系统。

2. 确保已安装的安装包是最新的。

    ```bash
    $ sudo dnf update
    ```

3. 添加 `yum` 源。

    ```bash
    $ sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
    [dockerrepo]
    name=Docker Repository
    baseurl=https://yum.dockerproject.org/repo/main/fedora/$releasever/
    enabled=1
    gpgcheck=1
    gpgkey=https://yum.dockerproject.org/gpg
    EOF
    ```

4. 安装Docker安装包。

    ```bash
    $ sudo dnf install docker-engine
    ```

5. 开启服务。

    ```bash
    $ sudo systemctl enable docker.service
    ```

6. 启动Docker守护进程。

    ```bash
    $ sudo systemctl start docker
    ```

7. 在一个容器中运行一个测试镜像来验证你的 `docker` 是否正确安装。

    ```bash
     $ sudo docker run --rm hello-world

     Unable to find image 'hello-world:latest' locally
     latest: Pulling from library/hello-world
     c04b14da8d14: Pull complete
     Digest: sha256:0256e8a36e2070f7bf2d0b0763dbabdd67798512411de4cdcf9431a1feb60fd9
     Status: Downloaded newer image for hello-world:latest

     Hello from Docker!
     This message shows that your installation appears to be working correctly.

     To generate this message, Docker took the following steps:
      1. The Docker client contacted the Docker daemon.
      2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
      3. The Docker daemon created a new container from that image which runs the
         executable that produces the output you are currently reading.
      4. The Docker daemon streamed that output to the Docker client, which sent it
         to your terminal.

     To try something more ambitious, you can run an Ubuntu container with:
      $ docker run -it ubuntu bash

     Share images, automate workflows, and more with a free Docker Hub account:
      https://hub.docker.com

     For more examples and ideas, visit:
      https://docs.docker.com/engine/userguide/
    ```

如果你想添加HTTP代理，设置另一个存放Docker运行时文件目录或者磁盘，或者其他个性化设置，阅读我们Systemd文章[customize your Systemd Docker daemon options](https://docs.docker.com/engine/admin/systemd/)。

### Install with the script[](https://docs.docker.com/engine/installation/linux/fedora/#install-with-the-script)

你可以使用同样的安装程序位所有版本的Fedora

1. 使用具有 `sudo` 或 `root` 权限的用户登录你的系统。

2. 确保你的已安装的软件包是最新的。

    ```bash
    $ sudo dnf update
    ```

3. 运行Docker 安装脚本。

    ```bash
    $ curl -fsSL https://get.docker.com/ | sh
    ```

    这个脚本添加 `docker.repo`仓库和安装Docker。

4. 开启服务。

    ```bash
    $ sudo systemctl enable docker.service
    ```

5. 开启Docker守护进程。

    ```bash
    $ sudo systemctl start docker
    ```

6. 在一个容器中运行一个测试镜像来验证你的 `docker` 是否正确安装。

    ```bash
    $ sudo docker run hello-world
    ```

如果你想添加HTTP代理，设置另一个存放Docker运行时文件目录或者磁盘，或者其他个性化设置，阅读我们Systemd文章[customize your Systemd Docker daemon options](https://docs.docker.com/engine/admin/systemd/)。

## Create a docker group[](https://docs.docker.com/engine/installation/linux/fedora/#create-a-docker-group)

 `docker` 守护进程绑定在一个Unix socket 来代替TCP端口。 默认情况下 Unix socket 属于 `root` 用户和其它具有 `sudo` 权限的用户。因此，`docker` 守护进程总是使用`root` 用户运行。

为避免每次使用 `docker` 命令都要添加`sudo`，创建一个叫做 `docker` 的Unix 用户组并使用它。当`docker` 守护进程启动，`docker` 用户组会分配Unix socket的读写权限。

> **警告**：`docker` 用户组等同于 `root` 用户;  更多关于他和系统安装之间的冲突，查看[*Docker Daemon Attack Surface*](https://docs.docker.com/engine/security/security/#docker-daemon-attack-surface)。

创建 `docker` 用户组和添加用户：

1. 使用具有 `sudo` 权限的用户登录系统。

2. 创建 `docker` 用户组。

    ```bash
    $ sudo groupadd docker
    ```

3. 添加你的用户到 `docker` 用户组。

    ```bash
    $ sudo usermod -aG docker $USER
    ```

4.  重新登录用户。

     确保你的用户拥有正确的权限。

5. 使用没有 `sudo` 的命令运行 `docker` 来验证你的工作。

    ```bash
    $ docker run hello-world
    ```

## Start the docker daemon at boot[](https://docs.docker.com/engine/installation/linux/fedora/#start-the-docker-daemon-at-boot)

配置Docker守护进程开机自启动：

```bash
$ sudo systemctl enable docker
```

## Running Docker with a manually-defined network[](https://docs.docker.com/engine/installation/linux/fedora/#running-docker-with-a-manually-defined-network)

如果你通过219或者更高版本的`systemd`使用`systemd-network`手动的配置你的网络，你启动的Docker容器可能不能访问网络。从220版本开始，默认的网络 (`net.ipv4.conf.<interface>.forwarding`)转发设置为*off*。这个设置阻止IP转发。这也和启用`net.ipv4.conf.all.forwarding`设置的Docker容器冲突。

为了解决这个问题，编辑`<interface>.network`文件在你Docker宿主机上`/usr/lib/systemd/network/` (ex: `/usr/lib/systemd/network/80-container-host0.network`) 添加以下文件块：

```bash
[Network]
...
IPForward=kernel
# OR
IPForward=true
...
```

这些配置像期望的那样允许从容器中进行IP转发。

## Uninstall[](https://docs.docker.com/engine/installation/linux/fedora/#uninstall)

你可以使用`dnf`卸载Docker软件。

1. 列出已安装的Docker安装包。

    ```bash
    $ dnf list installed | grep docker
    docker-engine.x86_64     1.7.1-0.1.fc21 @/docker-engine-1.7.1-0.1.fc21.el7.x86_64
    ```

2. 移除这些包。

    ```bash
    $ sudo dnf -y remove docker-engine.x86_64
    ```

    这条命令不会移除你的镜像，容器，数据卷或用户创建的配置文件在你的主机上。

3. 要删除所有的镜像，容器和数据卷运行如下命令：

    ```bash
    $ rm -rf /var/lib/docker
    ```

4. 定位和删除任何用户创建的配置文件。
