# CRUX Linux[](https://docs.docker.com/engine/installation/linux/cruxlinux/#crux-linux)

在CRUX Linux上安装Docker可以使用官方[contrib](http://crux.nu/portdb/?a=repo&q=contrib) 的ports：

* docker

`docker` ports会构建和安装最新版的Docker。

## Installation[](https://docs.docker.com/engine/installation/linux/cruxlinux/#installation)

假设你启用了contrib，更新你的ports树和安装docker：

```bash
$ sudo prt-get depinst docker
```

## Kernel requirements[](https://docs.docker.com/engine/installation/linux/cruxlinux/#kernel-requirements)

要使用**CRUX+Docker** 主机你必须确保你的Kernel内核已经启用保证Docker守护进程正常运行的模块。

请阅读 `README`:

```bash
$ sudo prt-get readme docker
```

`docker` port安装一个由Docker建设者为检查内核配置是否适用Docker主机所提供的`contrib/check-config.sh`脚本。

要检查内核配置运行：

```bash
$ /usr/share/docker/check-config.sh
```

## Starting Docker[](https://docs.docker.com/engine/installation/linux/cruxlinux/#starting-docker)

这里有一个为Docker创建的rc脚本。来开启Docker服务：

```bash
$ sudo /etc/rc.d/docker start
```

在系统启动时开启：

* 编辑 `/etc/rc.conf`
* 把 `docker` 放进 `SERVICES=(...)` 在 `net`后面。

## Images[](https://docs.docker.com/engine/installation/linux/cruxlinux/#images)

有一个CRUX镜像作为Docker“官方库”的一部分。要使用这个镜像建大的拉取它或者在`Dockerfile(s)`的`FROM`行使用它。

```bash
$ docker pull crux
$ docker run -i -t crux
```

这里也有用户贡献的 [CRUX based image(s)](https://hub.docker.com/_/crux/)在Docker Hub。

## Uninstallation[](https://docs.docker.com/engine/installation/linux/cruxlinux/#uninstallation)

要卸载Docker安装包：

```bash
$ sudo prt-get remove docker
```

上面的命令不会移除镜像，容器，磁盘和用户创建的配置文件在你的主机上。如果你希望删除所有的镜像，容器，磁盘命令如下：

```bash
$ rm -rf /var/lib/docker
```

你必需手动的删除用户配置文件。

## Issues[](https://docs.docker.com/engine/installation/linux/cruxlinux/#issues)

如果你有任何问题可以在 [CRUX Bug Tracker](http://crux.nu/bugs/)提交bug。

## Support[](https://docs.docker.com/engine/installation/linux/cruxlinux/#support)

联系 [CRUX Mailing List](http://crux.nu/Main/MailingLists) 寻求帮助或者加入CRUX的 [IRC Channels](http://crux.nu/Main/IrcChannels)。在 [FreeNode](http://freenode.net/) IRC 网络。
