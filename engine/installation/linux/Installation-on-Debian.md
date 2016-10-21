# Debian[](https://docs.docker.com/engine/installation/linux/debian/#debian)

Docker支持以下的Debian版本：

* [*Debian testing stretch (64-bit)*](https://docs.docker.com/engine/installation/linux/debian/#debian-wheezy-stable-7-x-64-bit)
* [*Debian 8.0 Jessie (64-bit)*](https://docs.docker.com/engine/installation/linux/debian/#debian-jessie-80-64-bit)
* [*Debian 7.7 Wheezy (64-bit)*](https://docs.docker.com/engine/installation/linux/debian/#debian-wheezy-stable-7-x-64-bit) (backports required)

> **注意**: 如果你之前使用`APT`安装过Docker，确保你的`APT`源更新为最新的`APT`仓库。

## Prerequisites[](https://docs.docker.com/engine/installation/linux/debian/#prerequisites)

Docker需要任一的64位Debian版本。另外，你的内核版本必须至少是3.10。3.10或更新的版本也是可接受的。

3.10以前的内核缺少Docker容器运行的一些功能。这些老的版本已知有很多致使数据丢失的bug，并且在一定的条件下频繁的崩溃。

要检查你的内核版本，打开终端使用  `uname -r`  命令打印你的内核版本：

    ```bash
    $ uname -r
    3.11.0-15-generic
    ```

另外，对于Debian Wheezy的用户，backports 必须可用。 在Wheezy中启用backports：

1. 使用具有 `sudo` 或 `root` 权限的用户登陆你的系统。

2. 打开 `/etc/apt/sources.list.d/backports.list` 文件。

    如果没有，创建一个。

3. 移除所有已存在的内容。

4. 为backports添加一些内容在Debian Wheezy.

    内容示例：

    ```bash
    deb http://http.debian.net/debian wheezy-backports main
    ```

5. 更新包信息。

    ```bash
     $ apt-get update
    ```

### Update your apt repository[](https://docs.docker.com/engine/installation/linux/debian/#update-your-apt-repository)

Docker的 `APT` 仓库包含Docker 1.7.1 和更高版本。设置 `APT` 使用最新的仓库：

1. 如果你没有这么做，使用具有`sudo` 或 `root` 权限的用户登录你的系统。

2. 打开一个终端窗口。

3. 清楚所有老的仓库。

    ```bash
    $ apt-get purge "lxc-docker*"
    $ apt-get purge "docker.io*"
    ```

4. 更新包信息，确保APT工作在`https`方法，已经安装并且CA 证书。

    ```bash
    $ apt-get update
    $ apt-get install apt-transport-https ca-certificates
    ```

5. 添加新的 `GPG` 密钥。

    ```bash
    $ apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
    ```

6. 打开文件`/etc/apt/sources.list.d/docker.list`。

    如果文件不存在，创建一个。

7. 移除所有已存在的内容。

8. 为你的Debian系统添加一些内容。

    可能的内容如下：

    * On Debian Wheezy

        ```bash
        deb https://apt.dockerproject.org/repo debian-wheezy main
        ```

    * On Debian Jessie

        ```bash
        deb https://apt.dockerproject.org/repo debian-jessie main
        ```

    * On Debian Stretch/Sid

        ```bash
        deb https://apt.dockerproject.org/repo debian-stretch main
        ```

    > **注意**: Docker 并没有提供安装包给所有的架构。 你可以每天在https://master.dockerproject.org查看最新的二进制包。 在多架构系统上安装Docker,，需要添加 `[arch=...]`节点。 点击 [Debian Multiarch wiki](https://wiki.debian.org/Multiarch/HOWTO#Setting_up_apt_sources) 获取更多细节。

9. 保存并关闭文件。

10. 更新 `APT` 包索引。

    ```bash
    $ apt-get update
    ```

11. 验证 `APT` 是否从正确的仓库拉取。

    ```bash
    $ apt-cache policy docker-engine
    ```

    从现在开始当你运行`apt-get upgrade`，`APT`从新的仓库拉取。

## Install Docker[](https://docs.docker.com/engine/installation/linux/debian/#install-docker)

安装Docker之前，确保你已经正确设置你的`APT`仓库。

1. 更新 `APT` 包索引。

    ```bash
    $ sudo apt-get update
    ```

2. 安装Docker。

    ```bash
    $ sudo apt-get install docker-engine
    ```

3. 开启 `docker` 守护进程。

    ```bash
    $ sudo service docker start
    ```

4. 验证 `docker` 是否正确安装。

    ```bash
    $ sudo docker run hello-world
    ```

    这条命令下载一个测试镜像并且在一个容器中运行它。当这个容器运行时, 他会打印一些信息然后退出。

## Giving non-root access[](https://docs.docker.com/engine/installation/linux/debian/#giving-non-root-access)

`docker` 守护进程绑定在一个Unix socket 来代替TCP端口。 默认情况下 Unix socket 属于 `root` 用户。因此，`docker` 守护进程总是使用`root` 用户运行。因此你可以通过`sudo`访问它。

如果你（或者你的Docker安装者）创建一个叫做`docker`的用户组并添加了一些用户到这个用户组，然后`docker` 用户组会分配Unix socket的读写权限当守护进程运行的时候。`docker` 守护进程必须总是以root用户运行，但是如果你通过`docker`用户组的用户运行一个`docker`客户端时你不需要再所有的客户端命令前加`sudo`。从Docker0.9.0开始你可以使用 `-G` 标志去指代一个替换组。

> **警告**:  `docker` 组 (或通过 `-G` 指定的组) 等同于 `root`； 详情查阅 [*Docker Daemon Attack Surface*](https://docs.docker.com/engine/security/security/#docker-daemon-attack-surface) 。

**Example:**

```bash
# Add the docker group if it doesn't already exist.
$ sudo groupadd docker

# Add the connected user "${USER}" to the docker group.
# Change the user name to match your preferred user.
# You may have to logout and log back in again for
# this to take effect.
$ sudo gpasswd -a ${USER} docker

# Restart the Docker daemon.
$ sudo service docker restart
```

## Upgrade Docker[](https://docs.docker.com/engine/installation/linux/debian/#upgrade-docker)

使用 `apt-get`安装最新版Docker：

```bash
$ apt-get upgrade docker-engine
```

## Uninstall[](https://docs.docker.com/engine/installation/linux/debian/#uninstall)

卸载Docker安装包：

```bash
$ sudo apt-get purge docker-engine
```

卸载不再需要的Docker安装包和依赖：

```bash
$ sudo apt-get autoremove --purge docker-engine
```

上面的命令不会移除镜像，容器，磁盘和用户创建的配置文件在你的主机上。如果你希望删除所有的镜像，容器，磁盘命令如下：

```bash
$ rm -rf /var/lib/docker
```

你必需手动的删除用户配置文件。

## What next?[](https://docs.docker.com/engine/installation/linux/debian/#what-next)

继续 [User Guide](https://docs.docker.com/engine/userguide/).
