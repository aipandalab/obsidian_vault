这是为你整理的来自 [Programming with Mosh](https://www.youtube.com/watch?v=pTFZFxd4hOI) 的 **Docker 新手入门教程** 中文文字稿。为了方便阅读，内容已转化为清晰的 Markdown 结构，并根据视频内容分为了两个核心部分：**Docker 核心概念** 与 **Linux 命令行基础**。

---

# Docker 新手入门教程（完整文字稿）

## 第一部分：Docker 核心基础

### 1. 课程介绍与前置知识 [00:01在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=1)

欢迎来到 Docker 终极课程。本教程将带你从零开始掌握 Docker，从基础概念一直到高级工作流，让你在软件开发中能像专家一样运用它。

- **实战目标**：我们将从一个简单的项目入手，随后使用 Docker 运行并部署一个包含前端、后端和数据库的全栈应用程序。
    
- **前置要求**：不需要任何 Docker 先修知识，但建议具备至少 3 个月的编程经验。你需要了解前端、后端、API、数据库等基本概念，并熟悉 Git 的基础操作（如 `git clone`, `commit`, `push`）。
    
- **学习建议**：本课程极具实战性，建议在观看时记录关键词，并在每节课后对照笔记亲自动手操作。
    

### 2. 什么是 Docker 及其重要性 [03:16在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=196)

Docker 是一个用于以一致的方式**构建、运行和交付（Ship）应用程序**的平台。

- **解决的痛点**：你可能常遇到“在我的电脑上运行正常，但在别人或服务器上就崩溃了”的情况。这通常是因为缺少文件、软件版本不一致（例如本地用 Node v14，服务器是 Node v9）或环境配置不同导致的。
    
- **Docker 的解决方案**：Docker 可以将你的应用程序连同它所需的所有依赖（如特定版本的 Node、MongoDB 等）打包在一起。只要你的电脑能运行，它就一定能在测试和生产环境的任何 Docker 机器上完美运行。
    
- **团队协作优势**：新员工加入团队后，无需花费半天时间配置复杂的本地环境。只需运行 Docker 指令，Docker 就会自动在一个名为容器（Container）的隔离环境中下载并运行所有依赖项。
    
- **环境清理**：当不再需要某个项目时，可以一键将其与所有依赖项安全删除，绝不会污染你的宿主机。
    

### 3. 容器（Containers）与虚拟机（VMs）的区别 [06:31在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=391)

- **虚拟机（Virtual Machine）**：是对物理硬件的抽象。它通过 Hypervisor（如 VirtualBox、VMware、Hyper-V）在同一台物理机上运行多个操作系统。
    
    - _缺点_：每个虚拟机都需要一份完整的操作系统拷贝，占用大量 CPU、内存和磁盘空间，且启动速度慢（通常需要几分钟）。
        
- **容器（Container）**：同样提供环境隔离，但非常轻量。**所有容器共享宿主机的操作系统内核**。
    
    - _优点_：不需要为每个容器授权和打补丁，启动速度极快（通常在 1 秒以内），且不占用固定的硬件切片。一台机器上可以轻松并行运行几十甚至上百个容器。
        

### 4. Docker 架构原理 [09:45在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=585)

Docker 采用 **客户端-服务器（Client-Server）** 架构：

- **Docker 客户端**：通过 REST API 向服务端发送指令。
    
- **Docker 服务端（Docker Engine）**：在后台运行，负责构建和运行容器。
    
- **内核共享机制**：容器技术依赖于操作系统内核（Kernel）。Linux 机器只能运行 Linux 容器；而 Windows 10/11 由于内置了 WSL（Linux 子系统内核），因此可以同时运行 Windows 和 Linux 容器；Mac 系统则会通过一个轻量级的 Linux 虚拟机来支持 Linux 容器的运行。
    

### 5. 安装 Docker [11:59在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=719)

- 请前往 [Docker 官方文档](https://docs.docker.com/get-docker/) 下载适用于 Mac、Windows 或 Linux 的 Docker Desktop/Engine。
    
- **注意事项**：Windows 用户需确保启用了 Hyper-V 和容器功能，如遇到 WSL 提示，需按照要求升级 Microsoft 提供的 Linux 内核更新包。
    
- **启动验证**：安装完成后必须确保 Docker 进程已在后台启动，在终端输入以下命令验证：
    
    Bash
    
    ```
    docker version
    ```
    

### 6. Docker 开发工作流与实战演练 [15:34在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=934)

在实际开发中，我们的工作流程如下：

1. **编写代码**：创建一个名为 `hello-docker` 的目录，并在其中编写一个简单的 `app.js`（内容：`console.log("hello")`）。
    
2. **编写 Dockerfile** [19:37在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=1177)：这是一个纯文本文件，用来定义应用的打包步骤：
    
    Dockerfile
    
    ```
    FROM node:alpine
    WORKDIR /app
    COPY . /app
    CMD ["node", "app.js"]
    ```
    
3. **构建镜像（Image）** [22:20在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=1340)：镜像是应用的只读模板。使用以下命令构建：
    
    Bash
    
    ```
    docker build -t hello-docker .
    ```
    
    你可以通过 `docker image ls` 或 `docker images` 查看本地已生成的镜像。由于使用了轻量级的 `alpine` 基础镜像，整体大小仅有 112MB 左右。
    
4. **运行容器** [24:23在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=1463)：基于该镜像启动一个独立的隔离进程：
    
    Bash
    
    ```
    docker run hello-docker
    ```
    
5. **发布与共享**：我们可以将镜像推送到类似于 GitHub 的 Docker 镜像托管中心 **Docker Hub**（例如作者发布的 `codewithmosh/hello-docker`）。
    
6. **云端测试** [24:55在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=1495)：通过在线工具（如 Play with Docker 平台），在没有任何本地依赖的干净环境中，直接运行以下命令即可拉取并执行该应用：
    
    Bash
    
    ```
    docker run codewithmosh/hello-docker
    ```
    

---

## 第二部分：Linux 命令行基础

### 1. 为什么学 Docker 必须要懂 Linux？ [27:59在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=1679)

Docker 的底层基石是 Linux 的概念。为了能够高效地排查故障、阅读网上的技术教程，即使你是 Windows 用户，也必须掌握最基础的 Linux 命令。

### 2. Linux 发行版（Distros）简介 [28:51在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=1731)

Linux 是开源的，因此拥有超过一千种不同的发行版，用于满足不同的场景需求（如 Ubuntu、Debian、Alpine、CentOS 等）。本教程将以最流行的 **Ubuntu** 为例进行演示。

### 3. 启动并交互 Linux 容器 [29:56在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=1796)

我们可以通过一行命令直接启动一个 Ubuntu 容器并进入交互模式：

Bash

```
docker run -it ubuntu
```

- `-it`：表示开启交互式（Interactive）终端。
    
- **Shell 提示符解析**（如 `root@fe321a4b5c6d:/#`）：
    
    - `root`：当前登录的用户（拥有最高权限）。
        
    - `fe321a4b5c6d`：当前容器的 ID（即主机名）。
        
    - `/`：当前所在的根目录。
        
    - `#`：代表最高权限符号（普通用户显示为 `$`）。
        
- **基本特性与快捷键**：
    
    - Linux 严格**区分大小写**（例如执行大写的 `ECHO` 会报错）。
        
    - 执行 `echo $0` 可以查看到当前运行的 Shell 程序路径为 `/bin/bash`。
        
    - **键盘上下键**：可上下翻阅历史输入的命令。
        
    - **`history`**：查看执行过的命令历史。使用 `!加数字`（如 `!2`）可以快速重新运行历史中对应编号的命令。
        

### 4. 包管理器 `apt` 详解 [35:08在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=2108)

在 Ubuntu 中，我们使用高级包工具 `apt`（在线教程中也常写作 `apt-get`）来管理软件。

- **重要安全步骤**：在安装任何新软件之前，必须先更新本地的软件包数据库：
    
    Bash
    
    ```
    apt update
    ```
    
- **安装软件**（以超轻量文本编辑器 `nano` 为例）：
    
    Bash
    
    ```
    apt install nano
    ```
    
- **卸载软件**：
    
    Bash
    
    ```
    apt remove nano
    ```
    

### 5. Linux 文件系统结构 [38:43在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=2323)

Linux 的文件系统是一个单根树状结构（从 `/` 开始），这与 Windows 的盘符概念（C盘、D盘）完全不同。一些常见的标准目录包括：

- `/bin`：存放二进制可执行程序（如 `pwd`, `echo` 等命令）。
    
- `/etc`：存放系统的文本配置文件（Editable Text Configuration）。
    
- `/home`：普通用户的家目录。
    
- `/root`：超级管理员 root 的特有家目录。
    
- `/var`：存放经常变化的文件（如系统日志 log、应用数据）。
    
- `/dev`、`/proc`：分别代表设备驱动和正在运行的系统进程（Linux 中“一切皆文件”）。
    

### 6. 文件系统导航与目录切换 [40:41在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=2441)

- **`pwd`**：打印当前工作目录（Print Working Directory）。
    
- **`ls`**：列出当前目录下的内容。
    
    - `ls -1`：每行只显示一个文件/目录。
        
    - `ls -l`：长格式输出，显示文件权限、所有者、大小及修改时间等详细信息。
        
- **`cd`**：切换目录。
    
    - 可以使用**相对路径**或**绝对路径**（以 `/` 开头的路径）。
        
    - **Tab 键**：用于快速自动补全路径。如果按一次没反应，连按两次可以列出所有匹配项。
        
    - `cd ..`：返回上一级目录。
        
    - `cd ~`（或直接键入 `cd`）：快速跳转到当前用户的**家目录**（Home Directory）。
        

### 7. 文件与目录的基本操作 [45:00在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=2700)

- **`mkdir <目录名>`**：创建新目录。
    
- **`mv <旧名> <新名或新路径>`**：重命名文件/目录，或移动它们的位置。
    
- **`touch <文件名>`**：创建一个新的空文件（支持一次性创建多个，如 `touch file1 file2`）。
    
- **`rm <文件名>`**：删除文件（支持使用通配符，如 `rm file*` 删除所有以 file 开头的文件）。
    
- **`rm -r <目录名>`**：**递归删除**一个目录及其内部的所有子文件和子目录。
    

### 8. 查看与编辑文件内容 [48:27在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=2907)

- **`nano <文件名>`**：在终端打开文本编辑器。编辑完成后按 `Ctrl + X`，再输入 `Y` 并回车即可保存退出。
    
- **`cat <文件名>`**：在终端直接连接并打印出整个文件的内容（适合短文件）。
    
- **`more <文件名>`**：分页查看长文件。按**空格键**向下翻页，按**回车键**逐行下滚，按 `Q` 退出。缺陷是不能向上滚动。
    
- **`less <文件名>`**（需通过 `apt install less` 安装）：更现代的分页查看器。完美支持使用**键盘上下方向键**自由地向上或向下滚动查看。
    
- **`head -n 5 <文件名>`**：仅查看文件的前 5 行。
    
- **`tail -n 5 <文件名>`**：仅查看文件的最后 5 行。
    

### 9. 输入输出重定向（Redirection） [52:22在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=3142)

在 Linux 中，默认的标准输出是屏幕，标准输入是键盘。我们可以通过操作符来改变它们：

- **`>`（覆盖重定向）**：将命令的输出流从屏幕导向并写入到一个文件中。
    
    - _示例 1_：复制文件内容。
        
        Bash
        
        ```
        cat file1.txt > file2.txt
        ```
        
    - _示例 2_：利用 `cat` 合并多个文件。
        
        Bash
        
        ```
        cat file1.txt file2.txt > combined.txt
        ```
        
    - _示例 3_：不打开编辑器，直接向文件写入单行文本。
        
        Bash
        
        ```
        echo "hello" > hello.txt
        ```
        
- **实战练习解法** [54:40在新窗口中打开](http://www.youtube.com/watch?v=pTFZFxd4hOI&t=3280)：将 `/etc` 目录的长格式列表保存到文件中：
    
    Bash
    
    ```
    ls -l /etc > files.txt
    ```
    

---

> 💡 **提示**：本教程为 Mosh 发布的公开基础试听版。如果想深入学习如何在真实生产环境中部署包含前后端分离与自动化测试的完整全栈 Docker 体系，可前往其官方学校 [codewithmosh.com](https://codewithmosh.com/) 查看完整课程。