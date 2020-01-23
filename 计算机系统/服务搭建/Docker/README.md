# Docker

Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker's methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between wirting code and running it in production.

Docker是一个用于开发，交付和运行应用程序的开放平台。Docker使您能够将应用程序与基础架构分开，从而可以快速交付软件。借助Docker，您可以以与管理应用程序相同的方式来管理基础架构。通过利用Docker的快速交付，测试和部署代码的方法，您可以大大减少编写代码和在生产环境中运行代码之间的延迟。



***Docker平台***

Docker提供了在松散隔离的环境（称为容器）中打包和运行应用程序的功能。隔离和安全性使您可以在给定主机上同时运行多个容器。容器是轻量级的，因为它们不需要管理程序的额外负担，而是直接在主机的内核中运行。这意味着与使用虚拟机相比，您可以在给定的硬件组合上运行更多的容器。您甚至可以在实际上是虚拟机的主机中运行Docker容器！

Docker提供了工具和平台来管理容器的生命周期：

- 使用容器开发应用程序及其支持组件。
- 容器成为分发和测试应用程序的单元。
- 准备就绪后，可以将应用程序作为容器或协调服务部署到生产环境中。无论您的生产环境是本地数据中心，云提供商还是两者的混合，其工作原理都相同。



***Docker引擎***

* daemon
* REST API
* CLI



![](https://docs.docker.com/engine/images/engine-components-flow.png)

CLI使用Docker REST API通过脚本或直接CLI命令控制或与Docker守护程序交互。许多其他Docker应用程序都使用基础API和CLI。

守护程序创建和管理Docker *对象*，例如图像，容器，网络和卷。



***Docker架构***

Docker使用客户端-服务器架构。Docker *客户端*与Docker *守护进程*进行对话，该*守护进程*完成了构建，运行和分发Docker容器的繁重工作。Docker客户端和守护程序*可以* 在同一系统上运行，或者您可以将Docker客户端连接到远程Docker守护程序。Docker客户端和守护程序在UNIX套接字或网络接口上使用REST API进行通信。

![](https://docs.docker.com/engine/images/architecture.svg)



*Docker守护进程*

Docker守护程序（`dockerd`）侦听Docker API请求并管理Docker对象，例如图像，容器，网络和卷。守护程序还可以与其他守护程序通信以管理Docker服务。

*Docker CLI*

Docker客户端（`docker`）是许多Docker用户与Docker交互的主要方式。当您使用诸如之类的命令时`docker run`，客户端会将这些命令发送到`dockerd`，以执行这些命令。该`docker`命令使用Docker API。Docker客户端可以与多个守护程序通信。

*Docker注册中心*

A Docker *registry* stores Docker images. Docker Hub is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default. You can even run your own private registry. If you use Docker Datacenter (DDC), it includes Docker Trusted Registry (DTR).

When you use the `docker pull` or `docker run` commands, the required images are pulled from your configured registry. When you use the `docker push` command, your image is pushed to your configured registry.





*Docker objects*

* images
* containers
* networks
* volumes
* plugins
* other objects

When you use Docker, you are creating and using images, containers, networks, volumes, plugins, and other objects. 



*IMAGES*

An *image* is a read-only template with instructions for creating a Docker container. Often, an image is *based on* another image, with some additional customization. For example, you may build an image which is based on the `ubuntu` image, but installs the Apache web server and your application, as well as the configuration details needed to make your application run.

You might create your own images or you might only use those created by others and published in a registry. To build your own image, you create a *Dockerfile* with a simple syntax for defining the steps needed to create the image and run it. Each instruction in a Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt. This is part of what makes images so lightweight, small, and fast, when compared to other virtualization technologies.



*CONTAINERS*

A container is a runnable instance of an image. You can create, start, stop, move, or delete a container using the Docker API or CLI. You can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.

By default, a container is relatively well isolated from other containers and its host machine. You can control how isolated a container’s network, storage, or other underlying subsystems are from other containers or from the host machine.

A container is defined by its image as well as any configuration options you provide to it when you create or start it. When a container is removed, any changes to its state that are not stored in persistent storage disappear.

>##### Example `docker run` command
>
>The following command runs an `ubuntu` container, attaches interactively to your local command-line session, and runs `/bin/bash`.
>
>```
>$ docker run -i -t ubuntu /bin/bash
>```
>
>When you run this command, the following happens (assuming you are using the default registry configuration):
>
>1. If you do not have the `ubuntu` image locally, Docker pulls it from your configured registry, as though you had run `docker pull ubuntu` manually.
>2. Docker creates a new container, as though you had run a `docker container create` command manually.
>3. Docker allocates a read-write filesystem to the container, as its final layer. This allows a running container to create or modify files and directories in its local filesystem.
>4. Docker creates a network interface to connect the container to the default network, since you did not specify any networking options. This includes assigning an IP address to the container. By default, containers can connect to external networks using the host machine’s network connection.
>5. Docker starts the container and executes `/bin/bash`. Because the container is running interactively and attached to your terminal (due to the `-i` and `-t` flags), you can provide input using your keyboard while the output is logged to your terminal.
>6. When you type `exit` to terminate the `/bin/bash` command, the container stops but is not removed. You can start it again or remove it.



*SERVICES*

Services allow you to scale containers across multiple Docker daemons, which all work together as a *swarm* with multiple *managers* and *workers*. Each member of a swarm is a Docker daemon, and the daemons all communicate using the Docker API. A service allows you to define the desired state, such as the number of replicas of the service that must be available at any given time. By default, the service is load-balanced across all worker nodes. To the consumer, the Docker service appears to be a single application. Docker Engine supports swarm mode in Docker 1.12 and higher.



***The underlying technology***

Docker is written in [Go](https://golang.org/) and takes advantage of several features of the Linux kernel to deliver its functionality.

* namepaces
* cgroup
* unionfs
* container formats





## 使用示例





## Image镜像管理

当运行容器时，使用的镜像如果在本地中不存在，docker 就会自动从 docker 镜像仓库中下载，默认是从 Docker Hub 公共镜像源下载。

* 管理和使用本地镜像
* 创建镜像



#### 1.	列出本地镜像

**docker images [OPTIONS] [REPOSITORY[:TAG]]**

**docker image ls [OPTIONS] [REPOSITORY[:TAG]]**

> ## Options
>
> | Name, shorthand | Default | Description                                         |
> | --------------- | ------- | --------------------------------------------------- |
> | `--all , -a`    |         | Show all images (default hides intermediate images) |
> | `--digests`     |         | Show digests                                        |
> | `--filter , -f` |         | Filter output based on conditions provided          |
> | `--format`      |         | Pretty-print images using a Go template             |
> | `--no-trunc`    |         | Don’t truncate output                               |
> | `--quiet , -q`  |         | Only show numeric IDs                               |

> ### Filtering
>
> The filtering flag (`-f` or `--filter`) format is of “key=value”.
>
> The currently supported filters are:
>
> - dangling (boolean - true or false)
> - label (`label=` or `label==`)
> - before (`[:]`, `` or ``) - filter images created before given id or references
> - since (`[:]`, `` or ``) - filter images created since given id or references
> - reference (pattern of an image reference) - filter images whose reference matches the specified pattern

> ### Format the output
>
> The formatting option (`--format`) will pretty print container output using a Go template.
>
> Valid placeholders for the Go template are listed below:
>
> | Placeholder     | Description                              |
> | :-------------- | :--------------------------------------- |
> | `.ID`           | Image ID                                 |
> | `.Repository`   | Image repository                         |
> | `.Tag`          | Image tag                                |
> | `.Digest`       | Image digest                             |
> | `.CreatedSince` | Elapsed time since the image was created |
> | `.CreatedAt`    | Time when the image was created          |
> | `.Size`         | Image disk size                          |

Image diget 不等于 Image ID，它们是两个不同的概念。

```sh
# List the most recently created images
$ docker images

# List images by name and tag
$ docker images ubuntu   
# $ docker images ubuntu:12.02

# filter
$ docker images -f "dangling=true"
$ docker rmi $(docker images -f "dangling=true" -q)
$ docker images -f "before=ubuntu:12.02"
$ docker images -f "since=ubuntu:12.02"
$ docker images --filter=reference='busy*:*libc'
# 注意：*匹配不包含'/'字符，如果匹配 'g*/*' -> gitlab/gitlab-ce 
# 多个过滤
$ docker images --filter=reference='busy*:uclibc' --filter=reference='busy*:glibc'

# format
$ docker images --format "{{.ID}}: {{.Repository}}"
$ docker images --format "table {{.ID}}\t{{.Repository}}\t{{.Tag}}"
```



> **注意**
>
> 镜像的 `ID` 唯一标识了镜像
>
> `TAG` 信息用来标记来自同一个仓库的不同镜像。仓库中有多个镜像，通过 `TAG` 信息来区分发行版本。
>
> 如果不指定具体的标记，则默认使用 `latest` 标记信息。



#### 2.	查找镜像

**docker search **

Search the Docker Hub for images

```sh
$ docker search ubuntu
```

> **NAME:** 镜像仓库源的名称
>
> **DESCRIPTION:** 镜像的描述
>
> **OFFICIAL:** 是否 docker 官方发布
>
> **stars:** 类似 Github 里面的 star，表示点赞、喜欢的意思。
>
> **AUTOMATED:** 自动构建。



#### 3.	获取镜像

**docker pull [OPTIONS] NAME[:TAG|@DIGEST]**

**docker image pull [OPTIONS] NAME[:TAG|@DIGEST]**

```sh
$ sudo docker pull ubuntu:12.04
Pulling repository ubuntu
ab8e2728644c: Pulling dependent layers
511136ea3c5a: Download complete
5f0ffaa9455e: Download complete
a300658979be: Download complete
904483ae0c30: Download complete
ffdaafd1ca50: Download complete
d047ae21eeaf: Download complete
```

下载过程中，会输出获取镜像的每一层信息。

该命令实际上相当于 `$ sudo docker pull registry.hub.docker.com/ubuntu:12.04` 命令，即从注册服务器`registry.hub.docker.com` 中的 `ubuntu` 仓库来下载标记为 `12.04` 的镜像。

有时候官方仓库注册服务器下载较慢，可以从其他仓库下载。 从其它仓库下载时需要指定完整的仓库注册服务器地址。例如

```sh
$ sudo docker pull dl.dockerpool.com:5000/ubuntu:12.04
Pulling dl.dockerpool.com:5000/ubuntu
ab8e2728644c: Pulling dependent layers
511136ea3c5a: Download complete
5f0ffaa9455e: Download complete
a300658979be: Download complete
904483ae0c30: Download complete
ffdaafd1ca50: Download complete
d047ae21eeaf: Download complete
```

完成后，即可随时使用该镜像了，例如创建一个容器，让其中运行 bash 应用。

```sh
$ sudo docker run -t -i ubuntu:12.04 /bin/bash
root@fe7fc4bd8fc9:/#
```



#### 4.	创建镜像











### 













## Docker容器



## 数据卷Volumes



## Network



















