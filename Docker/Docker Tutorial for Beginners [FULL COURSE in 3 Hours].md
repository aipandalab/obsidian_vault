这份 Markdown 格式的完整中文文字稿是根据视频 [[FULL COURSE] Docker Tutorial for Beginners](https://www.youtube.com/watch?v=3c-iBn73dDE) 的结构与听力内容翻译整理而成。

---

# Docker 初学者全套教程文字稿

## 01. 课程简介与概述 [00:01在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=1)

欢迎来到这门完整的 Docker 课程。到本课程结束时，你将对 Docker 的所有核心概念有深入的理解，并能宏观掌握 Docker 如何应用于整个软件开发流程中。

本课程结合了动画理论讲解与动手实操演示，帮助你在自己的项目中充满信心地使用 Docker。我们将涵盖以下主题：

- **基础概念**：Docker 是什么，它解决了什么问题，以及 Docker 与虚拟机的区别。
    
- **核心命令**：如何启动、停止和调试容器。
    
- **项目实战**：通过一个 Node.js + MongoDB 的 Demo 项目，演示如何在本地使用容器进行开发。
    
- **高效工具**：使用 Docker Compose 运行多容器服务。
    
- **镜像构建与发布**：编写 Dockerfile 构建自己的镜像，并将其推送到 AWS 的私有注册表（ECR）中。
    
- **数据持久化**：学习不同的 Docker Volume（卷）类型，并为项目配置持久化存储。
    

---

## 02. 什么是 Docker 与容器？ [01:58在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=118)

### 什么是容器？

容器是一种将应用程序及其所需的一切（包括依赖项和必要的配置）打包在一起的方法。这个包是高度**可移植的**，可以轻松地在开发团队内部或开发与运维（DevOps）团队之间共享和移动。这种独立隔离的环境带来了极高的开发与部署效率。

### 容器仓库（Container Repository）

容器镜像需要存储在特定的地方以便共享。

- **公有仓库（Public Repository）**：比如 [Docker Hub](https://www.google.com/search?q=https://hub.docker.com/)。它是官方的公共镜像中心，拥有超过10万个各种应用的镜像（如 Jenkins、PostgreSQL、Redis 等），任何人都可以免费下载使用。
    
- **私有仓库（Private Repository）**：许多公司会建立自己的内部仓库，用来存储包含商业机密的自定义应用镜像。
    

---

## 03. 容器如何改善开发与部署流程？ [04:58在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=298)

### 传统开发模式的痛点（Before Containers）

在没有容器前，开发团队的每个成员都需要直接在自己的操作系统上安装各种服务（例如 PostgreSQL、Redis）。

1. **多步骤安装**：安装步骤繁琐，很容易出错。
    
2. **环境不一致**：由于团队成员使用的操作系统不同（Windows、Mac、Linux），安装配置方法各异。
    
3. **服务冲突**：在一台机器上很难同时运行同一服务的不同版本。
    

### 容器化开发模式（After Containers）

使用容器后，你无需在宿主机系统上直接安装任何底层服务。

- 容器自带轻量级的隔离操作系统层（通常基于 Linux）。
    
- 开发者只需运行一条简单的 Docker 命令，即可同时完成下载和启动。
    
- 无论是 Windows、Mac 还是 Linux，执行的命令完全相同。你可以同时运行 PostgreSQL 9.6 和 10.10，各容器互不干扰。
    

### 传统部署 vs 容器化部署 [08:09在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=489)

- **以前**：开发将编译好的工件（如 `.jar` 文件）和一份长篇的“安装配置说明文档”交给运维（Operations）。运维照着文档在服务器上配置环境，经常因为沟通误解或环境差异导致部署失败（“在我的电脑上明明是好的”）。
    
- **现在**：开发和运维共同将应用及其全部依赖、配置封装进一个容器镜像中。部署时，服务器只需要运行一条 Docker 命令从仓库拉取并启动即可。服务器除了需要预先安装 Docker 运行时之外，不需要做任何复杂的环境配置。
    

---

## 04. Docker 与虚拟机的区别 [19:40在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=1180)

Docker 和虚拟机（VM）都是虚拟化工具，但它们虚拟化的操作系统层级完全不同：

|**特性**|**Docker (容器)**|**Virtual Machine (虚拟机)**|
|---|---|---|
|**虚拟化层级**|仅虚拟化**应用层**。它没有自己的内核，直接共享宿主机的操作系统内核。|虚拟化**整个操作系统**。包含应用层以及一个完整的客户操作系统内核（Guest OS）。|
|**镜像体积**|非常小（通常几兆到几百兆，如 Alpine Linux 仅 5MB）。|非常大（通常几吉字节 GB 级别）。|
|**启动速度**|秒级启动。|分钟级（需要引导完整的操作系统内核）。|
|**兼容性限制**|受到宿主机内核的制约。例如早期的 Windows/Mac 无法直接原生运行 Linux 容器（需要虚拟化过渡层）。|只要 Hypervisor 支持，可以在任何宿主机上运行任何 OS。|

---

## 05. Docker 安装指南 [23:53在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=1433)

Docker 分为**社区版（CE）和企业版（EE）**，初学者选择社区版即可。

- **Mac 安装** [27:14在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=1634)：前往官网下载 `Docker Desktop` 的 DMG 文件，双击并将 Docker 图标拖入 Applications 文件夹即可。
    
- **Windows 安装** [30:19在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=1819)：需要开启系统的硬件虚拟化支持（可在任务管理器 - 性能 - CPU 中查看）。满足条件后下载 `Docker Desktop` 安装包并按向导安装。
    
- **Linux 安装** [32:07在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=1927)：通过配置 Docker 的官方 APT/YUM 源，使用包管理器（如 `apt-get install docker-ce`）进行安装。
    
- _注：针对较老的 Windows 7/8 或旧版 Mac，以前需使用已被弃用的 Docker Toolbox [38:05在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=2285)，现在建议统一升级系统并使用 Docker Desktop。_
    

---

## 06. 核心 Docker 命令详解 [42:02在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=2522)

在操作前，请务必厘清镜像（Image）**与**容器（Container）的区别：镜像是不开机挂载的工件包（只读）；容器则是镜像运行起来后的实体环境（可读写）。

### 1. 镜像操作

- **拉取镜像**：
    
    Bash
    
    ```
    docker pull <image_name>:<tag>
    # 示例：docker pull redis:4.0 （如果不写 tag，默认下载 latest）
    ```
    
- **查看本地镜像**：
    
    Bash
    
    ```
    docker images
    ```
    

### 2. 容器启动与停止

- **创建并运行容器**（`docker run` 实际组合了 pull、create 和 start 三个动作）：
    
    Bash
    
    ```
    docker run -d -p 6000:6379 --name my-redis-app redis
    ```
    
    - `-d`：后台（分离模式）运行容器。
        
    - `-p 6000:6379`：**端口映射**。将宿主机（你的电脑）的 6000 端口绑定到容器内部的 6379 端口。
        
    - `--name`：为容器指定一个友好的别名。
        
- **停止与启动现有容器**：
    
    Bash
    
    ```
    docker stop <container_id_or_name>
    docker start <container_id_or_name>
    ```
    
- **查看容器状态**：
    
    Bash
    
    ```
    docker ps     # 查看当前正在运行的容器
    docker ps -a  # 查看所有容器（包括已停止的）
    ```
    

---

## 07. 容器调试与排错 [57:15在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=3435)

当应用无法连接或者容器报错时，有两款命令最常用：

- **查看容器日志**（`-f` 可用于持续追踪流日志）：
    
    Bash
    
    ```
    docker logs <container_name>
    docker logs -f <container_name>
    ```
    
- **进入容器内部终端**（执行交互式命令）：
    
    Bash
    
    ```
    docker exec -it <container_name> /bin/sh
    # 注：有些轻量级镜像（如 Alpine）没有安装 /bin/bash，此时需改用 /bin/sh
    ```
    
    进入后，你会看到容器内部独立的虚拟文件系统，输入 `exit` 即可退出。
    

---

## 08. 实战演练：Node.js + MongoDB 本地开发 [01:10:08在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=4208)

接下来，我们将演示如何建立一个用户档案管理网页。网页后端基于 Node.js（运行在本地宿主机上），数据需要持久化存储到 MongoDB 中。

### 理解 Docker 网络（Docker Network） [01:14:40在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=4480)

为了让多个容器互相通信，我们需要创建一个自定义的 Docker 网络。在同一个自定义网络中的容器，可以通过**容器名称**作为主机名直接通信，而无需暴露端口到宿主机。

1. **创建网络**：
    
    Bash
    
    ```
    docker network create mongo-network
    ```
    
2. **运行 MongoDB 容器**：
    
    Bash
    
    ```
    docker run -d \
      -p 27017:27017 \
      -e MONGO_INITDB_ROOT_USERNAME=admin \
      -e MONGO_INITDB_ROOT_PASSWORD=password \
      --name mongodb \
      --net mongo-network \
      mongo
    ```
    
    - `-e`：设置容器内的环境变量（配置了数据库的管理账号与密码）。
        
3. **运行 Mongo Express 网页管理后台**：
    
    Bash
    
    ```
    docker run -d \
      -p 8081:8081 \
      -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
      -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
      -e ME_CONFIG_MONGODB_SERVER=mongodb \
      --name mongo-express \
      --net mongo-network \
      mongo-express
    ```
    
    - 注意 `-e ME_CONFIG_MONGODB_SERVER=mongodb`：这里直接填写了上一步指定的 MongoDB 容器名。
        

此时，在浏览器打开 `http://localhost:8081` 即可进入图形化界面创建数据库。本地的 Node.js 代码可以通过配置 `mongodb://admin:password@localhost:27017` 来连接并读写该数据库。

---

## 09. 使用 Docker Compose 自动化多服务编排 [01:29:49在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=5389)

每次都手动输入这么长的 `docker run` 命令不仅繁琐，而且难以维护。通过 **Docker Compose**，我们可以将所有的配置写入一个 YAML 文件中。

创建名为 `mongo.yaml` 的文件：

YAML

```
version: '3'
services:
  mongodb:
    image: mongo
    ports:
      - 27017:27017
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=password

  mongo-express:
    image: mongo-express
    ports:
      - 8080:8081
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
      - ME_CONFIG_MONGODB_ADMINPASSWORD=password
      - ME_CONFIG_MONGODB_SERVER=mongodb
```

_注：Docker Compose 会自动为声明的所有服务创建一个默认网络，所以我们不需要手动配置 network 属性。_

- **一键启动所有服务**：
    
    Bash
    
    ```
    docker-compose -f mongo.yaml up -d
    ```
    
- **一键停止并销毁服务及网络**：
    
    Bash
    
    ```
    docker-compose -f mongo.yaml down
    ```
    

---

## 10. 编写 Dockerfile 构建自定义应用镜像 [01:42:02在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=6122)

现在，本地开发完成了，我们要将编写的 Node.js 应用打包成一个独立的 Docker 镜像，以便分发和部署。

在项目根目录下创建一个名为 `Dockerfile` 的文件（没有任何后缀，D大写）：

Dockerfile

```
# 1. 基础镜像：包含预安装的 Node.js 环境
FROM node:13-alpine

# 2. 设置容器内部的环境变量
ENV MONGO_DB_USERNAME=admin \
    MONGO_DB_PWD=password

# 3. 在容器内创建工作目录
RUN mkdir -p /home/app

# 4. 将宿主机当前目录下的 app 文件夹内容复制到容器的 /home/app 中
COPY ./app /home/app

# 5. 容器启动时默认执行的入口命令
CMD ["node", "/home/app/server.js"]
```

### 构建镜像：

Bash

```
docker build -t my-app:1.0 .
```

- `-t my-app:1.0`：指定镜像的名称和版本标签。
    
- `.`：代表当前上下文目录（Docker 会在当前目录下寻找 Dockerfile）。
    

---

## 11. 将镜像推送到 AWS ECR 私有仓库 [02:04:36在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=7476)

为了让测试服务器或其他同事能拿到这个镜像，需要将其上传到云端私有仓库（以 AWS ECR 为例）。

### 1. 镜像的完整命名规范 [02:09:29在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=7769)

一个非 Docker Hub 的独立仓库镜像，其完整名称格式为：

`[Registry域名]/[仓库/项目名称]:[标签]`

### 2. 推送步骤

1. **登录认证**：利用 AWS CLI 获取临时登录令牌并执行 `docker login`。
    
2. **给镜像打标记（重命名）**：
    
    Bash
    
    ```
    docker tag my-app:1.0 <aws_account_id>.dkr.ecr.<region>.amazonaws.com/my-app:1.0
    ```
    
3. **推送至云端**：
    
    Bash
    
    ```
    docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/my-app:1.0
    ```
    

后续如果代码有更新，只需本地重新 build 为 `my-app:1.1`，打上新的 tag 再次 push 即可。

---

## 12. 生产/测试服务器一键部署 [02:19:06在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=8346)

在测试或生产服务器上，我们同样编写一个 `docker-compose` 编排文件，将公共镜像（MongoDB）与我们托管在 AWS ECR 上的私有应用镜像组合起来：

YAML

```
version: '3'
services:
  my-app:
    image: <aws_account_id>.dkr.ecr.<region>.amazonaws.com/my-app:1.0
    ports:
      - 3000:3000
  
  mongodb:
    image: mongo
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=password
```

在服务器运行 `docker-compose up`，它就会自动从 AWS 下载你的专属应用，并从 Docker Hub 下载数据库，在服务器的网络中融为一体高效运转。

---

## 13. Docker Volumes：实现数据持久化 [02:27:26在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=8846)

### 为什么需要 Volume？

容器的文件系统是**临时的（Ephemeral）**。当你执行 `docker-compose down` 或容器因故崩溃重启后，容器内部数据库写入的所有数据都会彻底抹去。为了保存数据，必须引入 **Docker Volumes（数据卷）**。

### 原理

Volume 的本质是将宿主机上的物理文件系统目录挂载（Mount）到容器内部的虚拟文件系统目录中。两边的数据实时双向同步。当容器被销毁时，宿主机上的数据依然安全存在；新容器启动时重新挂载该目录，即可完美复原数据。

### 三种 Volume 类型 [02:29:32在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=8972)

1. **Host Volume**：手动指定宿主机的绝对路径（例如 `/home/user/db_data:/data/db`）。
    
2. **Anonymous Volume**：不指定宿主机路径，由 Docker 在后台自动随机生成 Hash 文件夹。难以追踪引用。
    
3. **Named Volume（推荐）**：给数据卷起一个明确的别名，由 Docker 管理其在宿主机上的具体存放路径。**这是生产环境的最佳实践**。
    

---

## 14. 卷实战配置（Named Volume） [02:33:03在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=9183)

更新我们的 `docker-compose` 文件，为 MongoDB 加上具名卷：

YAML

```
version: '3'
services:
  mongodb:
    image: mongo
    ports:
      - 27017:27017
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=password
    # 挂载具名卷到 MongoDB 默认的数据存储路径
    volumes:
      - mongo-data:/data/db

  mongo-express:
    image: mongo-express
    # 省略其他配置...

# 在宿主机顶层声明具名卷
volumes:
  mongo-data:
    driver: local
```

配置完成后，无论你重启容器多少次，在网页里录入的用户数据都将永久保存。

---

## 15. 课程总结与后续进阶 [02:45:13在新窗口中打开](http://www.youtube.com/watch?v=3c-iBn73dDE&t=9913)

恭喜你完成了 Docker 基础到实战的通关！

至此，你已经掌握了单机环境下容器的创建、编排、镜像分发及数据持久化。然而，当你的业务规模扩大，可能需要将成百上千个容器部署到多台不同的物理服务器上，依靠手动的 Docker Compose 就会力不从心。

- **下一步进阶建议**：深入学习容器编排工具 —— **Kubernetes (K8s)**。它能帮你自动实现多台服务器间的容器负载均衡、弹性伸缩以及故障自愈。