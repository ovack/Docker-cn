# Red Hat Enterprise Linux

Docker支持Red Hat Enterprise Linux 7。这篇指南使用Docker官方管理的发行包和安装工具，确保你获得的是最新的Docker。如果你希望使用Red Hat-managed packages安装Docker，查阅你的Red Hat发行版本。

## Prerequisites

Docker需要64位的操作系统和3.10以上的linux内核版本。
检查你当前的内核版本，打开终端使用 `uname -r` 命令打印你的内核版本：

```bash
$ uname -r
3.10.0-229.el7.x86_64
```

最后，我们非常推荐你更新整个系统。请记住，您的系统应该完全修补，已修复任何明确的内核错误。任何已报告的内核bug可能在最近的linux内核包中被修复。

## Install Docker Engine

这里有两种方式安装Docker Engine。你可以[使用`yum`包管理器安装](https://docs.docker.com/engine/installation/linux/rhel/#install-with-yum)。或者你可以使用 `curl` [`get.docker.com` site](https://docs.docker.com/engine/installation/linux/rhel/#install-with-the-script)。第二种方法运行一个安装脚本也是像`yum`包管理那样安装。

### Install with yum

1. 使用具有 `sudo` 或 `root` 权限的用户登陆你的系统。

2. 确保你的已经安装的包都是最新的。

    ```bash
    $ sudo yum update
    ```

3. 添加 `yum` 源。

    ```bash
    $ sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
    [dockerrepo]
    name=Docker Repository
    baseurl=https://yum.dockerproject.org/repo/main/centos/7/
    enabled=1
    gpgcheck=1
    gpgkey=https://yum.dockerproject.org/gpg
    EOF
    ```

4. 安装Docker。

    ```bash
    $ sudo yum install docker-engine
    ```

5. 开启服务。

    ```bash
    $ sudo systemctl enable docker.service
    ```

6. 开启Docker 守护进程。

    ```bash
    $ sudo systemctl start docker
    ```

7. 在容器中运行一个镜像来验证 `docker` 是否安装正确。

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

### Install with the script[](https://docs.docker.com/engine/installation/linux/rhel/#install-with-the-script)

1. 使用具有 `sudo` 或 `root` 权限的用户登陆你的系统。

2. 确保你的已经安装的包都是最新的。

    ```bash
    $ sudo yum update
    ```

3. 运行Docker安装脚本。

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

6. 在容器中运行一个镜像来验证 `docker` 是否安装正确。

    ```bash
    $ sudo docker run hello-world
    ```

如果你想添加HTTP代理，设置另一个存放Docker运行时文件目录或者磁盘，或者其他个性化设置，阅读我们Systemd文章[customize your Systemd Docker daemon options](https://docs.docker.com/engine/admin/systemd/)。

## Create a docker group[](https://docs.docker.com/engine/installation/linux/rhel/#create-a-docker-group)

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

## Start the docker daemon at boot[](https://docs.docker.com/engine/installation/linux/rhel/#start-the-docker-daemon-at-boot)

配置Docker守护进程开机自启动：

```bash
$ sudo systemctl enable docker
```

## Uninstall[](https://docs.docker.com/engine/installation/linux/rhel/#uninstall)

你可以使用 `yum` 卸载Docker 软件。

1. 列出已安装的Docker包。

    ```bash
    $ yum list installed | grep docker
    docker-engine.x86_64     1.7.1-0.1.el7@/docker-engine-1.7.1-0.1.el7.x86_64
    ```

2. 移除安装包。

    ```bash
    $ sudo yum -y remove docker-engine.x86_64
    ```

    上面的命令不会移除镜像，容器，磁盘和用户创建的配置文件在你的主机上。

3. 要删除镜像，容器，磁盘命令如下：

    ```bash
    $ rm -rf /var/lib/docker
    ```

4. 准确和查找所有用户创建的配置文件。
