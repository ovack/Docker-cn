# Ubuntu

Docker支持这些Ubuntu操作系统：

* Ubuntu Xenial 16.04 (LTS)
* Ubuntu Trusty 14.04 (LTS)
* Ubuntu Precise 12.04 (LTS)

这篇文章指导你使用Docker-managed的安装包和安装技巧来安装Docker。使用这些安装包确保你安装最新的Docker。如果你希望使用Ubuntu包管理器安装Docker，查看你的Ubuntu文档。

<!-- more -->

> **注意**: Ubuntu Utopic 14.10 and 15.04 在 Docker 的 `APT` 仓库但是很快将不再支持。

## Prerequisites

Docker需要一个不限版本的64位Ubuntu系统。另外你的内核版本必须在3.10以上。最近的3.10版本或者新的主要版本也是支持的。

3.10以前的内核缺少Docker容器运行的一些功能。这些老的版本已知有很多致使数据丢失的bug，并且在一定的条件下频繁的崩溃。

要检查你的内核版本，打开终端使用  `uname -r`  命令打印你的内核版本：

```bash
$ uname -r
3.11.0-15-generic
```

> **注意**：如果你之前使用 `APT` 安装过Docker， 请确保你已经更新过 `APT` 源。

### Update your apt sources

Docker的 `APT` 仓库包含 1.7.1 和更高的Docker版本。 设置 `APT` 使用安装包在新的仓库：

1. 使用具有 `sudo` or `root` 权限的用户登录你的系统。

2. 打开终端窗口。

3. 更新包信息, 确保 APT 工作在 `https` 模式，并且已经安装CA 证书。

    ```bash
    $ sudo apt-get update
    $ sudo apt-get install apt-transport-https ca-certificates
    ```

4. 添加新的 `GPG` 密钥。

    ```bash
     $ sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
    ```

5. 打开文件 `/etc/apt/sources.list.d/docker.list` 在你喜爱的编辑器。

    如果没有这个文件就创建它。

6. 清除所有内容。

7. 添加一些内容为你的Ubuntu 操作系统。

    可能的内容如下：

    * On Ubuntu Precise 12.04 (LTS)

        ```bash
        deb https://apt.dockerproject.org/repo ubuntu-precise main
        ```

    * On Ubuntu Trusty 14.04 (LTS)

        ```bash
        deb https://apt.dockerproject.org/repo ubuntu-trusty main
        ```

    * Ubuntu Xenial 16.04 (LTS)

        ```bash
        deb https://apt.dockerproject.org/repo ubuntu-xenial main
        ```

    > **注意**: Docker 并没有提供安装包给所有的架构。 你可以每天在https://master.dockerproject.org查看最新的二进制包。 在多架构系统上安装Docker,，需要添加 `[arch=...]`节点。 点击 [Debian Multiarch wiki](https://wiki.debian.org/Multiarch/HOWTO#Setting_up_apt_sources) 获取更多细节。

8. 保存并关闭  `/etc/apt/sources.list.d/docker.list` 文件。

9. 更新 `APT` 包索引。

    ```bash
    $ sudo apt-get update
    ```

10. 清除旧的仓库。

    ```bash
    $ sudo apt-get purge lxc-docker
    ```

11. 验证 `APT` 是否从正确的仓库拉取。

    ```bash
    $ apt-cache policy docker-engine
    ```

    从现在开始当你运行 `apt-get upgrade`，`APT` 从新的仓库拉取。

### Prerequisites by Ubuntu Version

* Ubuntu Xenial 16.04 (LTS)
* Ubuntu Trusty 14.04 (LTS)

对于Ubuntu Trusty，and Xenial，我们推荐安装 `linux-image-extra-*` 内核安装包。`linux-image-extra-*` 安装包允许你使用 `aufs` 存储驱动。

安装 `linux-image-extra-*` 步骤:

1. 在你的Ubuntu主机上打开终端。

2. 更新你的包管理器。

    ```bash
    $ sudo apt-get update
    ```

3. 安装推荐的包。

    ```bash
    $ sudo apt-get install linux-image-extra-$(uname -r) linux-image-extra-virtual
    ```

4. 安装Docker。

#### Ubuntu Precise 12.04 (LTS)

对于 Ubuntu Precise，Docker需要3.13内核版本。 如果你的内核版本低于3.13, 你必须更新内核。更具下面的表格查看你的环境需要安装哪些安装包:

| 安装包 | 描述 |
| :-- | :-- |
| **linux-image-generic-lts-trusty** | Generic Linux kernel image. 这个内核内建了运行Docker需要的AUFS。 |
| **linux-headers-generic-lts-trusty** | 像ZFS 和 VirtualBox guest additions基于这个包。如果你没有为你的内核安装这些headers，你可以跳过这些headers在"trusty" 内核。 如果你不确定是否安装，你最好安装一下。 |
| **xserver-xorg-lts-trusty** | 在没有图形环境的可选. **必需** 当运行Docker在一个图形界面。 |
| **libgl1-mesa-glx-lts-trusty** | 去了解更多安装这个包的原因, 月度backported kernels安装指南, 特别是 [LTS Enablement Stack](https://wiki.ubuntu.com/Kernel/LTSEnablementStack) — 在每个版本的第5条提到。 |

更新你的内核和安装额外的包, 操作如下：

1. 在你的Ubuntu主机上打开终端。

2. 更新你的包管理器。

    ```bash
    $ sudo apt-get update
    ```

3. 安装必需的和额外的安装包。

    ```bash
    $ sudo apt-get install linux-image-generic-lts-trusty
    ```

    取决于你的环境，你可能要安装比前面表格上要多的包。

4. 重启你的主机。

    ```bash
    $ sudo reboot
    ```

5. 当你的机器重启之后，安装Docker。

## Install

确保在你的Ububtu环境安装了前面提到的软件。

然后，按下列步骤安装：

1. 使用具有 `sudo` 权限的用户登录你的Ubuntu系统。

2. 更新你的 `APT` 包索引。

    ```bash
    $ sudo apt-get update
    ```

3. 安装 Docker。

    ```bash
    $ sudo apt-get install docker-engine
    ```

4. 开启 `docker` 守护进程。

    ```bash
    $ sudo service docker start
    ```

5. 验证 `docker` 是否安装正确。

    ```bash
    $ sudo docker run hello-world
    ```

    这条命令下载一个测试镜像并且在一个容器中运行它。当这个容器运行时, 他会打印一些信息然后退出。

## Optional configurations

这部分包含一些额外的软件使你的Ubuntu更好的为Docker工作。

* [Create a docker group](https://docs.docker.com/engine/installation/linux/ubuntulinux/#create-a-docker-group)
* [Adjust memory and swap accounting](https://docs.docker.com/engine/installation/linux/ubuntulinux/#adjust-memory-and-swap-accounting)
* [Enable UFW forwarding](https://docs.docker.com/engine/installation/linux/ubuntulinux/#enable-ufw-forwarding)
* [Configure a DNS server for use by Docker](https://docs.docker.com/engine/installation/linux/ubuntulinux/#configure-a-dns-server-for-use-by-docker)
* [Configure Docker to start on boot](https://docs.docker.com/engine/installation/linux/ubuntulinux/#configure-docker-to-start-on-boot)

### Create a Docker group

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

   如果失败会显示下面的信息：

    ```bash
    Cannot connect to the Docker daemon. Is 'docker daemon' running on this host?
    ```

    查看 `DOCKER_HOST` 环境变量是否设置，如果没有重新设置它。

### Adjust memory and swap accounting

当用户运行Docker，它们会看到下面的信息：

```bash
WARNING: Your kernel does not support cgroup swap limit. WARNING: Your
kernel does not support swap limit capabilities. Limitation discarded.
```

阻止这些信息，在你的系统上开启 memory and swap accounting。开启 memory and swap accounting 会导致内存占用和效率下降，即时没有运行Docker。 大概会占用总内存的1%。效率大概下降10%。

开启 memory and swap on system 使用 GNU GRUB (GNU GRand Unified Bootloader)，步骤如下:

1. 使用具有 `sudo` 权限的用户登录你的系统。

2. 编辑 `/etc/default/grub` 文件。

3. 设置 `GRUB_CMDLINE_LINUX` 的值如下：

    ```bash
    GRUB_CMDLINE_LINUX="cgroup_enable=memory swapaccount=1"
    ```

4. 保存并关闭文件。

5. 更新 GRUB。

    ```bash
    $ sudo update-grub
    ```

6. 重启你的系统

### Enable UFW forwarding

如果你使用 [UFW (Uncomplicated Firewall)](https://help.ubuntu.com/community/UFW) 在你运行Docker的主机上，你需要额外的配置。Docker 使用桥连来管理容器的网络。默认情况下， UFW 关闭所有的转发流量。因此，当Docker运行时开启了UFW， 你必需设置UFW的转发策略。

另外， UFW的默认设置是阻挡所有的流入流量。如果你希望你的每一个容器都能在Docker端口和远程的主机上通信。如果TLS启用，Docker的端口默认是 `2376` 否则则是 `2375` 。 如果TLS禁止, 通信会被拒绝。 默认情况下，Docker 运行在TLS关闭的情况下。

配置UFW和允许Docker端口流入流量：

1. 使用具有 `sudo` 权限的用户登录系统。

2. 验证UFW是否安装和启用。

    ```bash
    $ sudo ufw status
    ```

3. 编辑 `/etc/default/ufw` 文件

    ```bash
    $ sudo nano /etc/default/ufw
    ```

4. 设置 `DEFAULT_FORWARD_POLICY` 策略为:

    ```bash
    DEFAULT_FORWARD_POLICY="ACCEPT"
    ```

5. 保存并关闭文件。

6. 重新加载UFW。

    ```bash
    $ sudo ufw reload
    ```

7. 允许Docker端口的连接。

    ```bash
    $ sudo ufw allow 2375/tcp
    ```

### Configure a DNS server for use by Docker

在运行Ubuntu或者Ubuntu派生的桌面系统上一般使用 `127.0.0.1` 作为默认的`nameserver`在配置文件 `/etc/resolv.conf` 中。 NetworkManager 也设置 `dnsmasq` 使用真实的DNS servers和设置`nameserver 127.0.0.1` 在文件 /`etc/resolv.conf`中。

当使用这些配置运行容器在桌面机器中，Docker 用户可见下面的警告：

```bash
WARNING: Local (127.0.0.1) DNS resolver found in resolv.conf and containers
can't use it. Using default external servers : [8.8.8.8 8.8.4.4]
```

导致这个警告的的原因是Docker容器不能使用本地的DNS nameserver。取而代之，Docker使用外在的nameserver。

为了避免这些警告，你可以为你的Docker容器特别指定DNS server。或者，你可以禁止`dnsmasq`在NetworkManager。可是，禁止`dnsmasq`可能会导致DNS解析速度变慢。

在下面的指南描述了怎么配置Docker守护进程在Ubuntu 14.10或者更低的版本。Ubuntu 15.04或者以上版本使用`systemd` 作为启动和服务管理。查阅 [control and configure Docker with systemd](https://docs.docker.com/engine/admin/systemd/#custom-docker-daemon-options) 去配置一个`systemd`管理的守护进程。

为Docker指定具体的 DNS server：

1. 使用 `sudo` 权限的用户登录Ubuntu系统。

2. 编辑文件 `/etc/default/docker` 。

    ```bash
    $ sudo nano /etc/default/docker
    ```

3. 为Docker添加一项设置。

    ```bash
    DOCKER_OPTS="--dns 8.8.8.8"
    ```

    替换 `8.8.8.8` 为一个本地 DNS server 比如 `192.168.1.1`。你也可以指定多个DNS servers。 用空格把他们区分开，例如:

    ```bash
    --dns 8.8.8.8 --dns 192.168.1.1
    ```

    > **警告**: 如果你在一个网络多变的笔记本上做这些配置, 要确保选择一个公共的 DNS server.

4. 保存文件。

5. 重启Docker 守护进程。

    ```bash
    $ sudo service docker restart
    ```

**Or, as an alternative to the previous procedure,** 在NetworkManager里禁止 `dnsmasq`  （这可能导致你网速变慢）。

1. 编辑文件 `/etc/NetworkManager/NetworkManager.conf` 。

    ```bash
    $ sudo nano /etc/NetworkManager/NetworkManager.conf
    ```

2. 注释 `dns=dnsmasq` 这一行：

    ```bash
    dns=dnsmasq
    ```

3. 保存文件。

4. 重启NetworkManager 和 Docker。

    ```bash
    $ sudo restart network-manager
   $ sudo restart docker
    ```

### Configure Docker to start on boot

Ubuntu 使用 `systemd` 作为他的boot and service 管理器在 `15.04` 版本以上，使用`upstart` 在版本 `14.10`及以下。

对于 `15.04` 及以上版本，要配置`docker` 守护进程在启动时就运行，执行：

```bash
$ sudo systemctl enable docker
```

对于 `14.10` 及其以下版本在安装的过程中已经自动配置 `upstart` 开机自动启动。

## Upgrade Docker

使用 `apt-get`安装最新版本的Docker:

```bash
$ sudo apt-get upgrade docker-engine
```

## Uninstallation

卸载Docker安装包：

```bash
$ sudo apt-get purge docker-engine
```

要卸载Docker安装包和依赖，下面的命令已不再需要：

```bash
$ sudo apt-get autoremove --purge docker-engine
```

上面的命令不会移除镜像，容器，磁盘和用户创建的配置文件在你的主机上。如果你希望删除所有的镜像，容器，磁盘命令如下：

```bash
$ rm -rf /var/lib/docker
```

你必需手动的删除用户配置文件。
