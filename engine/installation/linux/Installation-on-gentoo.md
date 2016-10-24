# Gentoo[](https://docs.docker.com/engine/installation/linux/gentoolinux/#gentoo)

安装Docker到Gentoo Linux可以通过两种方式完成：**official**途径和`docker-overlay`途径。

官方项目页面[Gentoo Docker](https://wiki.gentoo.org/wiki/Project:Docker)。

## Official way[](https://docs.docker.com/engine/installation/linux/gentoolinux/#official-way)

我们推荐第一种方式直接使用官方的`app-emulation/docker`包，如果你在寻找稳定的体验。

如果这个ebuild发生任何问题，包括缺少的内核配置或依赖，打开一个bug在Gentoo [Bugzilla](https://bugs.gentoo.org/)分配给`docker AT gentoo DOT org` 或者加入和咨询在官方频道[IRC](http://webchat.freenode.net/?channels=%23gentoo-containers&uio=d4) 在Freenode网站。

## docker-overlay way[](https://docs.docker.com/engine/installation/linux/gentoolinux/#docker-overlay-way)

如果你在寻找一个`-bin` ebuild，一个即时的ebuild或者一个bleeding edge ebuild，使用，[docker-overlay](https://github.com/tianon/docker-overlay) 可以使用`app-portage/layman`添加。大部分精确的和最新为正确的安装和使用overlay的文档在[overlay](https://github.com/tianon/docker-overlay/blob/master/README.md#using-this-overlay)。

如果这个ebuild发生任何问题，包括缺少的内核配置或依赖，打开一个[issue](https://github.com/tianon/docker-overlay/issues)在`docker-overlay` 仓库或者ping`tianon`直接在`＃docker` IRC频道

## Installation[](https://docs.docker.com/engine/installation/linux/gentoolinux/#installation)

### Available USE flags[](https://docs.docker.com/engine/installation/linux/gentoolinux/#available-use-flags)

| 使用标记 | 默认 | 描述 |
| :-- | :-: | :-- |
| aufs |   | 为“aufs”图像驱动开启依赖，包含必需的内核标志。|
| btrfs |   | 为“btrfs”图像驱动开启依赖，包含必需的内核标志。|
| contrib | Yes | 安装额外的脚本和组件。 |
| device-mapper | Yes | 为“devicemapper”图像驱动开启依赖，包含必需的内核标志。 |
| doc |   | 添加额外的文档，比如API和Javadoc。我们推荐开启部分包。|
| vim-syntax |   |采用vim语法脚本。 |
| zsh-completion |   | 启用zsh完全支持。|

使用标记详情[tianon’s blog](https://tianon.github.io/post/2014/05/17/docker-on-gentoo.html)。

安装包应该正确的拉取必需的依赖和所有的内核选项。

```bash
$ sudo emerge -av app-emulation/docker
```

> 注意: 有时官方版本**Gentoo tree**和**docker-overlay**之间会有差异。
> 请耐心等待，最新版本将尽快传播。

## Starting Docker[](https://docs.docker.com/engine/installation/linux/gentoolinux/#starting-docker)

确保你正在运行的内核包含所有需要的模块和配置（和可选的device-mapper和AUFS或者Btrfs，取决于你使用的存储驱动）。

使用Docker， `docker`守护进程必须使用**root**运行。
要**non-root**的用户使用Docker，通过下列命令把你自己添加到**docker**组：

```bash
$ sudo groupadd docker
$ sudo usermod -a -G docker user
```

### OpenRC[](https://docs.docker.com/engine/installation/linux/gentoolinux/#openrc)

启动`docker`守护进程：

```bash
$ sudo /etc/init.d/docker start
```

在系统启动时运行：

```bash
$ sudo rc-update add docker default
```

### systemd[](https://docs.docker.com/engine/installation/linux/gentoolinux/#systemd)

开启`docker`守护进程：

```bash
$ sudo systemctl start docker
```

在系统启动时运行：

```bash
$ sudo systemctl enable docker
```

如果你想添加HTTP代理，设置另一个存放Docker运行时文件目录或者磁盘，或者其他个性化设置，阅读我们Systemd文章[customize your Systemd Docker daemon options](https://docs.docker.com/engine/admin/systemd/)。

## Uninstallation[](https://docs.docker.com/engine/installation/linux/gentoolinux/#uninstallation)

卸载Docker安装包：

```bash
$ sudo emerge -cav app-emulation/docker
```

卸载不需要的Docker安装包和依赖：

```bash
$ sudo emerge -C app-emulation/docker
```

上述命令不会删除主机上的图像，容器，卷或用户创建的配置文件。 如果要删除所有图像，容器和卷，请运行以下命令：

```bash
$ rm -rf /var/lib/docker
```

你必需手动的删除用户配置文件。
