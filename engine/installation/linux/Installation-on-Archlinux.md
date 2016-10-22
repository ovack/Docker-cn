# Arch Linux[](https://docs.docker.com/engine/installation/linux/archlinux/#arch-linux)

在Arch Linux上安装可以通过社区中的包来处理：

* [docker](https://www.archlinux.org/packages/community/x86_64/docker/)

或者下面的 AUR 包：

* [docker-git](https://aur.archlinux.org/packages/docker-git/)

docker安装包会安装最新版本的docker。docker-git 安装包是从最新的master分支上构建的。

## Dependencies[](https://docs.docker.com/engine/installation/linux/archlinux/#dependencies)

Docker依赖在包中指定的几个依赖包。核心依赖是：

* bridge-utils
* device-mapper
* iproute2
* sqlite

## Installation[](https://docs.docker.com/engine/installation/linux/archlinux/#installation)

对于普通包的一个简单的例子

```bash
$ sudo pacman -S docker
```

是所有需要的。

对于AUR 包执行：

```bash
$ yaourt -S docker-git
```

The instructions here assume **yaourt** is installed. See [Arch User Repository](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) for information on building and installing packages from the AUR if you have not done so before.
这篇指南假定已经安装**yaourt**。查看[Arch User Repository](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) 获取从AUR上构建和安装包，如果你之前没有这么做过。

## Starting Docker[](https://docs.docker.com/engine/installation/linux/archlinux/#starting-docker)

有一个为docker创建的systemd服务单元。开启docker服务：

```bash
$ sudo systemctl start docker
```

在系统上启动：


```bash
$ sudo systemctl enable docker
```

## Custom daemon options[](https://docs.docker.com/engine/installation/linux/archlinux/#custom-daemon-options)

如果你想添加HTTP代理，设置另一个存放Docker运行时文件目录或者磁盘，或者其他个性化设置，阅读我们Systemd文章[customize your Systemd Docker daemon options](https://docs.docker.com/engine/admin/systemd/)。

## Running Docker with a manually-defined network[](https://docs.docker.com/engine/installation/linux/archlinux/#running-docker-with-a-manually-defined-network)

如果你通过220或者更高版本的`systemd`使用`systemd-network`手动的配置你的网络，你启动的Docker容器可能不能访问网络。从220版本开始，默认的网络 (`net.ipv4.conf.<interface>.forwarding`)转发设置为*off*。这个设置阻止IP转发。这也和启用`net.ipv4.conf.all.forwarding`设置的Docker容器冲突。

To work around this, edit the `<interface>.network` file in `/etc/systemd/network/` on your Docker host add the following block:
为了解决这个问题，编辑`<interface>.network`文件在你Docker宿主机上`/etc/systemd/network/` 添加以下文件块：

```bash
[Network]
...
IPForward=kernel
...
```

此配置允许像预期那样从container进行IP转发。

## Uninstallation

卸载Docker安装包：

```bash
$ sudo pacman -R docker
```

卸载不需要的Docker安装包和依赖：

```bash
$ sudo pacman -Rns docker
```

上面的命令不会移除镜像，容器，磁盘和用户创建的配置文件在你的主机上。如果你希望删除所有的镜像，容器，磁盘命令如下：

```bash
$ rm -rf /var/lib/docker
```

你必需手动的删除用户配置文件。
