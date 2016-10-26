# openSUSE and SUSE Linux Enterprise[](https://docs.docker.com/engine/installation/linux/SUSE/#opensuse-and-suse-linux-enterprise)

这个页面提供在openSUSE 和 SUSE 系统安装和配置最新版本Docker引擎的指南。

> **注意:**你可以在[Open Build Service](https://build.opensuse.org/)上的[Virtualization:containers project](https://build.opensuse.org/project/show/Virtualization:containers) 找到最新的Docker版本。这个项目也分发其他Docker生态的其他安装包（例如，Docker Compose）。

## Prerequisites[](https://docs.docker.com/engine/installation/linux/SUSE/#prerequisites)

你必须运行64位架构系统。

## openSUSE[](https://docs.docker.com/engine/installation/linux/SUSE/#opensuse)

从13.2开始，Docker是官方openSUSE仓库的一部分。在你的系统上，不需要额外的仓库。

## SUSE Linux Enterprise[](https://docs.docker.com/engine/installation/linux/SUSE/#suse-linux-enterprise)

从SUSE Linux Enterprise 12 和最新版开始，Docker受SUSE官方支持。你可以找到最新支持的Docker安装包在`Container`模块里面。要开启这个模块，步骤如下：

1.  开始YaST，然后选择*Software > Software Repositories*。
2.  点击 *Add* 打开add-on窗口。
3.  选择 *Extensions and Module from Registration Server* 然后点击 *Next*。
4.  在可选扩展和模块列表，选择*Container Module*和点击*Next*。containers模块和他的仓库被添加到你的系统。
5.  如果你使用订阅管理工具，更新SMT server上的仓库列表。

另外执行下面命令：

```bash
$ sudo SUSEConnect -p sle-module-containers/12/x86_64 -r ''
>**Note:** currently the `-r ''` flag is required to avoid a known limitation of `SUSEConnect`.
```

[Virtualization:containers project](https://build.opensuse.org/project/show/Virtualization:containers) on the [Open Build Service](https://build.opensuse.org/)包含最新版的Docker安装包为SUSE Linux Enterprise。然而这些安装包**不支持**SUSE

### Install Docker[](https://docs.docker.com/engine/installation/linux/SUSE/#install-docker)

1.  安装Docker安装包：

    ```bash
    $ sudo zypper in docker
    ```

2.  开启Docker守护进程。

    ```bash
    $ sudo systemctl start docker
    ```

3.  测试已安装的Docker。

    ```bash
    $ sudo docker run hello-world
    ```

## Configure Docker boot options[](https://docs.docker.com/engine/installation/linux/SUSE/#configure-docker-boot-options)

你可以在openSUSE或者SUSE Linux Enterprise上使用下列步骤。在系统启动时开启`docker daemon`，设置如下：

```bash
$ sudo systemctl enable docker
```

`docker`安装包创建一个新叫做`docker`的组。除了`root`用户，必须要加入这个组才能和Docker守护进程通讯。你可以使用下面的命令添加用户到用户组：


```bash
sudo /usr/sbin/usermod -a -G docker <username>
```

一旦你添加一个用户，重新登录确保这个用户获得正确的权限。

## Enable external network access[](https://docs.docker.com/engine/installation/linux/SUSE/#enable-external-network-access)

如果你希望你的容器使用外部网络，你必须开启`net.ipv4.ip_forward`规则。为此，使用YaST。

对于openSUSE Tumbleweed和最新版本，定位到**System -> Network Settings -> Routing**菜单。对于 SUSE Linux Enterprise 12 和先前的 openSUSE 版本，定位到 **Network Devices -> Network Settings -> Routing** 菜单和勾选*Enable IPv4 Forwarding*框。

当网络由Network Manager处理时，代替YaST你必须手动编辑文件`/etc/sysconfig/SuSEfirewall2`，确保`FW_ROUTE`的值设置为`yes`：

```bash
FW_ROUTE="yes"
```

## Custom daemon options[](https://docs.docker.com/engine/installation/linux/SUSE/#custom-daemon-options)

如果你想添加HTTP代理，设置另一个存放Docker运行时文件目录或者磁盘，或者其他个性化设置，阅读我们Systemd文章[customize your Systemd Docker daemon options](https://docs.docker.com/engine/admin/systemd/)。

## Uninstallation[](https://docs.docker.com/engine/installation/linux/SUSE/#uninstallation)

卸载Docker安装包：

```bash
$ sudo zypper rm docker
```

上述命令不会删除主机上的图像，容器，卷或用户创建的配置文件。 如果要删除所有图像，容器和卷，请运行以下命令：

```bash
$ rm -rf /var/lib/docker
```

你必需手动的删除用户配置文件。

## Where to go from here[](https://docs.docker.com/engine/installation/linux/SUSE/#where-to-go-from-here)

你可以SUSE网站[Docker quick start guide](https://www.suse.com/documentation/sles-12/dockerquick/data/dockerquick.html)找到更多关于Docker运行在openSUSE或者SUSE Linux Enterprise的信息。这个文档是关于SUSE Linux Enterprise，但是同样适用于openSUSE。

继续 [User Guide](https://docs.docker.com/engine/userguide/)。


