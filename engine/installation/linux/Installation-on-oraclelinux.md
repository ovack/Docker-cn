# Oracle Linux[](https://docs.docker.com/engine/installation/linux/oracle/#oracle-linux)

Docker支持在Oracle Linux 6和7。把Docker安装在Oracle Linux你不需要Oracle Linux支持订阅。

## Prerequisites[](https://docs.docker.com/engine/installation/linux/oracle/#prerequisites)

由于当前Docker限制，Docker只能运行在x86_64架构上。Docker需要在Oracle Linux上使用Unbreakable Enterprise Kernel Release 4 (4.1.12)或更高版本。这个内核支持在Oracle Linux 6 和 7的Docker btrfs存储引擎。

## Install[](https://docs.docker.com/engine/installation/linux/oracle/#install)

> **注意**: 下面的程序的安装二进制包由Docker构建。Oracle Linux 支持不包括这些二进制包。要确保Oracle Linux 支持，请按照 [Oracle Linux documentation](https://docs.oracle.com/en/operating-systems/?tab=2)提供的安装指南。
> 为Oracle Linux 6 和 7的安装指南可以在[Chapter 2 of the Docker User's Guide](https://docs.oracle.com/cd/E52668_01/E75728/html/docker_install_upgrade.html)查看。

1. 使用具有 `sudo` 或 `root` 权限的用户登录你的系统。

2. 确保你现在的yum软件包是最新的。

    ```bash
    $ sudo yum update
    ```

3. 添加yum源。

    为版本6：

    ```bash
    $ sudo tee /etc/yum.repos.d/docker.repo <<-EOF
    [dockerrepo]
    name=Docker Repository
    baseurl=https://yum.dockerproject.org/repo/main/oraclelinux/6
    enabled=1
    gpgcheck=1
    gpgkey=https://yum.dockerproject.org/gpg
    EOF
    ```

    为版本7：

    ```bash
    $ cat >/etc/yum.repos.d/docker.repo <<-EOF
    [dockerrepo]
    name=Docker Repository
    baseurl=https://yum.dockerproject.org/repo/main/oraclelinux/7
    enabled=1
    gpgcheck=1
    gpgkey=https://yum.dockerproject.org/gpg
    EOF
    ```

4. 安装Docker安装包。

    ```bash
    $ sudo yum install docker-engine
    ```

5. 开启Docker守护进程。

    在Oracle Linux 6：

    ```bash
    $ sudo service docker start
    ```

    在Oracle Linux 7：

    ```bash
    $ sudo systemctl start docker.service
    ```

6. 在容器中运行一个镜像来验证 `docker` 是否安装正确。

    ```bash
    $ sudo docker run hello-world
    ```

## Optional configurations[](https://docs.docker.com/engine/installation/linux/oracle/#optional-configurations)

这部分包含可选的程序使你的Oracle Linux能够更好地和Docker一起工作。

* [Create a docker group](https://docs.docker.com/engine/installation/linux/oracle/#create-a-docker-group)
* [Configure Docker to start on boot](https://docs.docker.com/engine/installation/linux/oracle/#configure-docker-to-start-on-boot)
* [Use the btrfs storage engine](https://docs.docker.com/engine/installation/linux/oracle/#use-the-btrfs-storage-engine)

### Create a Docker group[](https://docs.docker.com/engine/installation/linux/oracle/#create-a-docker-group)

`docker` 守护进程绑定在一个Unix socket 来代替TCP端口。 默认情况下 Unix socket 属于 `root` 用户和其它具有 `sudo` 权限的用户。因此，`docker` 守护进程总是使用`root` 用户运行。

为避免每次使用 `docker` 命令都要添加`sudo`，创建一个叫做 `docker` 的Unix 用户组并使用它。当`docker` 守护进程启动，`docker` 用户组会分配Unix socket的读写权限。

> **警告**: `docker` 用户组等同于 `root` 用户;  更多关于他和系统安装之间的冲突，查看[*Docker Daemon Attack Surface*](https://docs.docker.com/engine/security/security/#docker-daemon-attack-surface)。
To create the `docker` group and add your user:

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

    如果失败会出现以下类似信息：

    ```bash
    Cannot connect to the Docker daemon. Is 'docker daemon' running on this host?
    ```

    检查 `DOCKER_HOST` 环境变量是否设置。如果设置了，重新设置它。

### Configure Docker to start on boot[](https://docs.docker.com/engine/installation/linux/oracle/#configure-docker-to-start-on-boot)

你可以配置Docker守护进程在开机时自启动。

在Oracle Linux 6：

```bash
$ sudo chkconfig docker on
```

在Oracle Linux 7：

```bash
$ sudo systemctl enable docker.service
```

如果你想添加HTTP代理，设置另一个存放Docker运行时文件目录或者磁盘，或者其他个性化设置，阅读我们Systemd文章[customize your Systemd Docker daemon options](https://docs.docker.com/engine/admin/systemd/)。

### Use the btrfs storage engine[](https://docs.docker.com/engine/installation/linux/oracle/#use-the-btrfs-storage-engine)

Docker支持在Oracle Linux 6 和 7上使用btrfs存储引擎。在开启btrfs支持之前，确保`/var/lib/docker`存储在一个btrfs-based文件系统上。查阅[Chapter 5](http://docs.oracle.com/cd/E37670_01/E37355/html/ol_btrfs.html) 关于 [Oracle Linux Administrator’s Solution Guide](http://docs.oracle.com/cd/E37670_01/E37355/html/index.html) 获取更多如何创建和挂载btrfs文件系统的细节。

在Oracle Linux上开启btrfs 支持：

1. 确保 `/var/lib/docker` 在一个btrfs文件系统上。

2. 编辑 `/etc/sysconfig/docker` 和为字段`OTHER_ARGS` 添加值`-s btrfs`。

3. 重新启动Docker守护进程：

## Uninstallation[](https://docs.docker.com/engine/installation/linux/oracle/#uninstallation)

卸载Docker 安装包：

```bash
$ sudo yum -y remove docker-engine
```

上述命令不会删除主机上的图像，容器，卷或用户创建的配置文件。 如果要删除所有图像，容器和卷，请运行以下命令：

```bash
$ rm -rf /var/lib/docker
```

你必需手动的删除用户配置文件。

## Known issues[](https://docs.docker.com/engine/installation/linux/oracle/#known-issues)

### Docker unmounts btrfs filesystem on shutdown[](https://docs.docker.com/engine/installation/linux/oracle/#docker-unmounts-btrfs-filesystem-on-shutdown)

如果你在btrfs存储系统上运行Docker引擎并停止Docker服务，他将在关闭过程中卸载btrfs系统。你在每次重启Docker服务时需要确保文件系统是否正确挂载。

在Oracle Linux 7，你可以使用`systemd.mount` 定义和修改Docker`systemd.service`依赖于btrfs挂载在系统级。

### SElinux support on Oracle Linux 7[](https://docs.docker.com/engine/installation/linux/oracle/#selinux-support-on-oracle-linux-7)

在文件`/etc/sysconfig/selinux`中必须将SElinux设置为`Permissive` 或者 `Disabled` 在Oracle Linux 7上使用btrfs存储。

## Further issues?[](https://docs.docker.com/engine/installation/linux/oracle/#further-issues)

如果你拥有Oracle Linux基本和高级支持订阅，你可以在 [My Oracle Support](https://support.oracle.com/)报告任何关于安装Docker的工单。

如果你没有Oracle Linux支持订阅，你可以使用[Oracle Linux Forum](https://community.oracle.com/community/server_%26_storage_systems/linux/oracle_linux) 社区支持。

