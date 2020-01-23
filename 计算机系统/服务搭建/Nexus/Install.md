

## Nexus是什么？

Nexus是一个存储库管理系统，在程序供应链中管理二进制库和构建组件。

![Universal Control](https://www.sonatype.com/hs-fs/hubfs/Repo%20Tour%202019/Platform_grey_line-trim.png?width=956&name=Platform_grey_line-trim.png)

在以上的通用控制系统里，它支持所有流行的存储库格式，这些格式分为4大类：

* 存储和发布，比如Maven，npm，Nuget，APT，YUM等
* 管理组件，binaries, containers, assemblies, and finished goods.
* Java生态支持
* 流行工具



# Install

### 1.	系统要求

对于主机系统，支持部分Windows、Linux和苹果操作系统，只要这些系统能够运行相应的Java版本，都可以很好地安装和运行Nexus。

Nexus也提供了Docker镜像，以供安装。

> 注意：如果是以Linux的系统来运行Nexus Repository Manage 3（NXRM 3），推荐创建一个'nexus'的用户来运行NXRM进程，这个用户必须能够shell。因为这样做更安全。

#### Java

Nexus Repository Manager 3 is a Java server application that requires a **Java 8** SE standard compatible runtime.

**Java runtime versions other than 8 are not supported - do not use them.**

**Only 64 bit Java is supported, do not use 32 bit Java.**

NXPM3 是一个Java应用，依赖Java 8 SE，并且需要使用64位的Java。

#### 计算机物理资源

Nexus平台的只要限制是IO（disk and network），相对CPU而言。

CPU推荐 8+（8线程及其以上），物理内存最小为8G。

硬盘存储空间尽量大些，最小500G，具体视使用情况而定，如果Nexus的格式是Docker和Maven，那么用完500G的存储空间是很容易的事情。

#### 更多细节

更多的细节可以参照以下说明：

https://help.sonatype.com/repomanager3/system-requirements#SystemRequirements-Docker



### 2.	下载

Nexus分为Pro和OSS版本，Pro是商业版，OSS是社区版。目前Nexus的最新主版本号为3，以前Nexus的主版本号为2。Nexus 3要比Nexus2多很多新功能，并且Nexus3是未来。建议使用Nexus 3的社区版。

> 注意：nexus-3.20版本，经测试，在登录输入登录名和密码时有bug，会导致死机。所以建议使用 nexus.3.15版本，或者nexus-3.20修复登录bug后的版本。

#### 下载地址

https://help.sonatype.com/repomanager3/download/download-archives---repository-manager-3



### 3.	安装

#### 3.1	准备工作

* Centos 7.9
* JDK 1.8
* [nexus-3.15.2-01-unix.tar.gz](http://download.sonatype.com/nexus/3/nexus-3.15.2-01-unix.tar.gz)



#### 3.2	安装

Nexus3依赖于64位的JAVA 1.8，所以在安装nexus3前需要确保已经安装Java1.8 64-Bit，安装完成后提示如下：

```
$ java -version
openjdk version "1.8.0_222-ea"
OpenJDK Runtime Environment (build 1.8.0_222-ea-b03)
OpenJDK 64-Bit Server VM (build 25.222-b03, mixed mode)
```

**安装nexus**

```sh
sudo mkdir /opt/nexus
sudo tar -xzvf nexus-3.15.2-01-unix.tar.gz -C /opt/nexus/
# 解压后在nexus里有两个目录：nexus-3.15.2-01和sonatype-work
# sonatype-work用于存放blob，即存储块

# 创建一个nexus用户，-M(--no-create-home) -r(--system)
sudo useradd -M -r nexus	
sudo usermod -d /opt/nexus/nexus-3.15.2901127
-01 nexus # 修改nexus的主目录
sudo chown -R nexus:nexus nexus-3.15.2-01 sonatype-work

# 运行nexus
cd /opt/nexus/nexus-3.15.2-01/bin
sudo ./nexus run
# 运行nexus会显示运行日志，运行成功后，火狐浏览器里输入网址：localhost:8081，即可显示nexus的运行主页面。
# 登录名为admin，登录密码admin123
```



#### 3.3	配置服务

##### init.d

```sh
vim /opt/nexus/nexus-3.15.2-01/bin/nexus.rc
# 在文件nexus.rc里追加一行：run_as_user="nexus"，保存退出。
sudo ln -s /opt/nexus/nexus-3.15.2-01/bin/nexus /etc/init.d/nexus

cd /etc/init.d
sudo chkconfig --add nexus
sudo chkconfig --levels 345 nexus on
suod service nexus start
```



##### systemd

创建一个文件 `nexus.service`，文件内容如下，然后将文件保存到目录`/etc/systemd/system`下。

```sh
[Unit]
Description=nexus service
After=network.target
  
[Service]
Type=forking
LimitNOFILE=65536
ExecStart=/opt/nexus/nexus-3.15.2-01/bin/nexus start
ExecStop=/opt/nexus/nexus-3.15.2-01/bin/nexus stop
User=nexus
Restart=on-abort
  
[Install]
WantedBy=multi-user.target
```

激活服务

```sh
sudo systemctl daemon-reload
sudo systemctl enable nexus.service
sudo systemctl start nexus.service
```





## 创建仓库

### 1.	仓库的类型

| 类型                | 作用                                |
| ------------------- | ----------------------------------- |
| hosted（宿主仓库）  | 存放公司私有的库和包                |
| proxy（代理仓库）   | 代理中央仓库的包                    |
| group（组仓库）     | 使用时连接组仓库，包含hosted和proxy |
| virtual（虚拟仓库） | 一般不用                            |



Nexus3搭建好后，默认会创建Maven和Nuget的仓库，如果需要创建其他仓库可以按照以下步骤：

#### 1.	创建Blob

Blob用于存储数据，而数据相关的元数据和信息则保存在数据库里。所以在创建仓库前需要创建blob。

![1Ct7Uf.md.png](https://s2.ax1x.com/2020/01/19/1Ct7Uf.md.png)



输入Name，Path会自动填写

![1CtTVP.md.png](https://s2.ax1x.com/2020/01/19/1CtTVP.md.png)

#### 2.	创建仓库

![1CtH58.md.png](https://s2.ax1x.com/2020/01/19/1CtH58.md.png)



输入相应字段信息，Blob store则选择自己在上面操作创建的blob即可。

[![1Ct5DI.md.png](https://s2.ax1x.com/2020/01/19/1Ct5DI.md.png)](https://imgchr.com/i/1Ct5DI)

创建好存储库，即可向存储库上传代码包等

![1CNgZq.png](https://s2.ax1x.com/2020/01/19/1CNgZq.png)

