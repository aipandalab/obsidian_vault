以下是视频 [How to Install Docker on Ubuntu: A Step-By-Step Guide](http://www.youtube.com/watch?v=cqbh-RneBlk) 的完整中文翻译文本稿：

---

**[00:00在新窗口中打开](http://www.youtube.com/watch?v=cqbh-RneBlk&t=0)** 嘿，大家好，欢迎回到我的频道。在这段视频中，我将一步步向大家演示如何在 Ubuntu 上安装 Docker。

**[00:05在新窗口中打开](http://www.youtube.com/watch?v=cqbh-RneBlk&t=5)** 首先，让我们确保拥有正确的 Ubuntu 版本。你需要一个 64 位版本的 Ubuntu，并且版本号应该在 16.04 或更高。

**[00:20在新窗口中打开](http://www.youtube.com/watch?v=cqbh-RneBlk&t=20)** 如果你不确定自己使用的是什么版本，可以通过运行以下命令来进行检查：

Bash

```
lsb_release -a
```

按下回车键。以我为例，我运行的是 Ubuntu Desktop 22.04 版本。

**[00:29在新窗口中打开](http://www.youtube.com/watch?v=cqbh-RneBlk&t=29)** 接下来，我们需要使用以下命令来更新我们的软件包数据库：

Bash

```
sudo apt get update
```

我现在输入我的密码。这可以确保我们能够获取到最新版本的软件包。

**[00:47在新窗口中打开](http://www.youtube.com/watch?v=cqbh-RneBlk&t=47)** 现在，让我们运行以下命令来安装 Docker 引擎：

Bash

```
sudo apt install docker.io
```

按下回车键，然后输入 `Y` 并按回车键继续。系统接下来会下载并安装 Docker 软件包。

**[01:04在新窗口中打开](http://www.youtube.com/watch?v=cqbh-RneBlk&t=64)** 好的，安装已经完成了。一旦安装结束，我们需要使用以下命令来启用 Docker 服务：

Bash

```
sudo systemctl enable docker
```

按下回车键。这可以确保每次我们在开机启动机器时，Docker 服务都会自动启动。

**[01:22在新窗口中打开](http://www.youtube.com/watch?v=cqbh-RneBlk&t=82)** 此外，我们还需要确保 Docker 服务正在运行。为此，你可以运行以下命令：

Bash

```
sudo systemctl status docker
```

太好了，你可以看到它显示为“active (running)”（处于激活并运行状态）。

**[01:35在新窗口中打开](http://www.youtube.com/watch?v=cqbh-RneBlk&t=95)** 万一它没有运行，你可以执行以下命令来启动 Docker 服务：

Bash

```
sudo systemctl start docker
```

**[01:45在新窗口中打开](http://www.youtube.com/watch?v=cqbh-RneBlk&t=105)** 最后，让我们通过运行一个名为 “hello-world” 的 Docker 容器，来测试我们的 Docker 安装是否成功。运行以下命令：

Bash

```
sudo docker run hello-world
```

按下回车键。如果一切设置正确，你应该会看到一条写着 “Hello from Docker!” 的消息。

**[02:04在新窗口中打开](http://www.youtube.com/watch?v=cqbh-RneBlk&t=124)** 就像我们在这里看到的一样。大功告成！现在你已经在你的 Ubuntu 机器上成功安装了 Docker。

**[02:10在新窗口中打开](http://www.youtube.com/watch?v=cqbh-RneBlk&t=130)** 感谢收看，请务必点赞并订阅以获取更多技术教程。