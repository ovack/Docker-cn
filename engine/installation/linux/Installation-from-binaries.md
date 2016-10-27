# Installation from binaries[](https://docs.docker.com/engine/installation/binaries/#installation-from-binaries)

**创建这篇指南的目的是为那些希望在多样化环境中运行Docker的hackers。**

在开始下面行动之前，你应该彻底检查一下已经打包的Docker 版本在你的发行版linux上是否可用。我们为多个发行版打包，并继续为更多的发行版打包。

## Check runtime dependencies[](https://docs.docker.com/engine/installation/binaries/#check-runtime-dependencies)

要正确的运行，Docker需要在运行环境安装下面的软件：

* iptables version 1.4 or later
* Git version 1.7 or later
* procps (or similar provider of a “ps” executable)
* XZ Utils 4.9 or later
* a [properly mounted](https://github.com/tianon/cgroupfs-mount/blob/master/cgroupfs-mount) cgroupfs hierarchy (having a single, all-encompassing “cgroup” mount point [is](https://github.com/docker/docker/issues/2683) [not](https://github.com/docker/docker/issues/3485) [sufficient](https://github.com/docker/docker/issues/4568))

## Check kernel dependencies[](https://docs.docker.com/engine/installation/binaries/#check-kernel-dependencies)

Docker在后台模式有特殊的内核需求。更多，在[*Installation*](https://docs.docker.com/engine/installation/#on-linux)检查你的发行版。

3.10以前的内核缺少Docker容器运行的一些功能。这些老的版本已知有很多致使数据丢失的bug，并且在一定的条件下频繁的崩溃。

建议使用3.10（或更新的维护版本）Linux内核的主要维护版本（3.x.y）。 使内核保持最新的版本将确保关键的内核错误得到修复。

> **警告**: 安装定制的内核和呢荷包可能不被你的发行版供应商支持。在安装内核包前请联系你的供应商确保其支持Docker。
> **警告**: 在一些发行版本上安装最新的内核可能还不够，可能其提供的包太旧和最新的内核冲突。

注意Docker有client模式，他可以运行在任何虚拟的Linux呢和上（它甚至可以运行在macOS！）。

## Enable AppArmor and SELinux when possible[](https://docs.docker.com/engine/installation/binaries/#enable-apparmor-and-selinux-when-possible)

请使用AppArmor或者SELinux如果你的linux发行版支持两者任意一个。这可以提高系统的安全性并阻止一些漏洞。你的发行版的文档应该提供如何开启建议的安全程序的步骤。

一些linux发行版开启AppArmor或者SELinux但是没有运行在必需的内核版本（3.10 或 newer）。更新这些内核到3.10或更新的版本不足以运行Docker和容器。系统提供的AppArmor / SELinux用户空间实用程序版本与内核之间的不兼容性可能会阻止Docker运行，启动容器或导致容器出现意外行为。

> **Warning**: If either of the security mechanisms is enabled, it should not be disabled to make Docker or its containers run. This will reduce security in that environment, lose support from the distribution’s vendor for the system, and might break regulations and security policies in heavily regulated environments.

## Get the Docker Engine binaries[](https://docs.docker.com/engine/installation/binaries/#get-the-docker-engine-binaries)

你可以下载最新版本或特别版本的二进制包。要获得一系列稳定版本的列表，查看 `docker/docker` [releases page](https://github.com/docker/docker/releases)。您可以通过将.md5和.sha 256分别附加到URL来获取MD5和SHA256。

### Get the Linux binaries[](https://docs.docker.com/engine/installation/binaries/#get-the-linux-binaries)

使用下面的链接下载最新版本：

```bash
https://get.docker.com/builds/Linux/i386/docker-latest.tgz
https://get.docker.com/builds/Linux/x86_64/docker-latest.tgz
```

要下载指定版本使用下面的url规则：

```bash
https://get.docker.com/builds/Linux/i386/docker-<version>.tgz
https://get.docker.com/builds/Linux/x86_64/docker-<version>.tgz
```

比如：

```bash
https://get.docker.com/builds/Linux/i386/docker-1.11.0.tgz
https://get.docker.com/builds/Linux/x86_64/docker-1.11.0.tgz
```

> **注意** 这些说明适用于Docker Engine 1.11及以上版本。 Engine 1.10和以下版本由一个二进制文件组成，这些版本的指令是不同的。 要安装1.10或更低版本，请按照中的说明进行操作[1.10 documentation](https://docs.docker.com/v1.10/engine/installation/binaries/)。

#### Install the Linux binaries

下载之后，把压缩包解压到你当前位置 `docker` 目录。

```bash
$ tar -xvzf docker-latest.tgz

docker/
docker/docker
docker/docker-containerd
docker/docker-containerd-ctr
docker/docker-containerd-shim
docker/docker-proxy
docker/docker-runc
docker/dockerd
```

Engine需要安装这些二进制包到你主机的 `$PATH`。例如安装这些二进制包到`/usr/bin` ：

```bash
$ mv docker/* /usr/bin/
```

> **注意**: 如果你已经安装过Engine在你的主机上，在你安装之前确保已经停止Engine（`killall docker`）和安装二进制包到同样的位置。你可以通过`dirname $(which docker)`命令查看当前Docker安装的位置。

#### Run the Engine daemon on Linux

你可以手动的开启Engine到后台模式使用：

```bash
$ sudo dockerd &
```

GitHub仓库包含一些示例脚本，你可以通过进程管理器（upstart或者systemd）来控制守护进程。你可以在[contrib directory](https://github.com/docker/docker/tree/master/contrib/init)找到这些脚本。

更多关于在守护进程模式下运行Engine，查阅 [daemon command](https://docs.docker.com/engine/reference/commandline/dockerd/) Engine命令行参考。

### Get the macOS binary[](https://docs.docker.com/engine/installation/binaries/#get-the-macos-binary)

macOS版二进制包晶晶是一个客户端。你不可以用它运行`docker`守护进程。为macOS下载最新版本的，使用下面链接：

```bash
https://get.docker.com/builds/Darwin/x86_64/docker-latest.tgz
```

要为macOS下载指定版本，使用下面的路径：

```bash
https://get.docker.com/builds/Darwin/x86_64/docker-<version>.tgz
```

例如：

```bash
https://get.docker.com/builds/Darwin/x86_64/docker-1.11.0.tgz
```

你可以通过双击下载的`.tgz`压缩文件或者在命令行使用`tar -xvzf docker-1.11.0.tgz`命令。客户端二进制包可以在任何位置执行。

### Get the Windows binary[](https://docs.docker.com/engine/installation/binaries/#get-the-windows-binary)

你只可以下载`1.9.1`以上的Windows二进制包。此外32-bit (`i386`)我二进制包紧紧是一个客户端，你不可以运行`docker`守护进程。64-bit 二进制包 (`x86_64`)既是客户端和守护进程。

使用下面的链接下载最新版Windows二进制包：

```bash
https://get.docker.com/builds/Windows/i386/docker-latest.zip
https://get.docker.com/builds/Windows/x86_64/docker-latest.zip
```

使用下面的链接下载指定版本的Windows二进制包：

```bash
https://get.docker.com/builds/Windows/i386/docker-<version>.zip
https://get.docker.com/builds/Windows/x86_64/docker-<version>.zip
```

例如：

```bash
https://get.docker.com/builds/Windows/i386/docker-1.11.0.zip
https://get.docker.com/builds/Windows/x86_64/docker-1.11.0.zip
```

> **注意** 这些指南是为了Engine 1.11 和更新版本。 未老版本的指南跟这略微不同。要安装 1.10 或以下版本查看下列指南 [1.10 documentation](https://docs.docker.com/v1.10/engine/installation/binaries/)。

## Giving non-root access[](https://docs.docker.com/engine/installation/binaries/#giving-non-root-access)

`docker` 守护进程总是使用root用户运行，`docker` 守护进程绑定在一个Unix socket 来代替TCP端口。 默认情况下 Unix socket 属于 `root` 用户。因此，你可以通过`sudo`来访问它。

为避免每次使用 `docker` 命令都要添加`sudo`，创建一个叫做 `docker` 的Unix 用户组并使用它。当`docker` 守护进程启动，`docker` 用户组会分配Unix socket的读写权限。

如果你（或者你的Docker安装者）创建一个叫做`docker`的用户组并添加了一些用户到这个用户组，然后`docker` 用户组会分配Unix socket的读写权限当守护进程运行的时候。`docker` 守护进程必须总是以root用户运行，但是如果你通过`docker`用户组的用户运行一个`docker`客户端时你不需要再所有的客户端命令前加`sudo`。从Docker0.9.0开始你可以使用 `-G` 标志去指代一个替换组。

> **警告**:  `docker` 组 (或通过 `-G` 指定的组) 等同于 `root`； 详情查阅 [*Docker Daemon Attack Surface*](https://docs.docker.com/engine/security/security/#docker-daemon-attack-surface) 。

## Upgrade Docker Engine[](https://docs.docker.com/engine/installation/binaries/#upgrade-docker-engine)

要手动的在linux上更新你的Docker Engine，首先要关掉docker守护进程：

```bash
$ killall docker
```

然后跟随 [regular installation steps](https://docs.docker.com/engine/installation/binaries/#get-the-linux-binaries).

## Next steps[](https://docs.docker.com/engine/installation/binaries/#next-steps)

继续 [User Guide](https://docs.docker.com/engine/userguide/).


