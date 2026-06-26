根据视频内容，为你整理并生成的 Markdown 格式中文文字稿如下：

---

# 视频文字稿：如何搭建完全本地化的 AI Agent | Hermes Desktop 与 Ollama

- **视频来源**: [Vasilij Nevlev | AiGentic Lab](https://www.youtube.com/watch?v=7qIfFVb06bc)
    
- **主讲人**: V（AI 咨询顾问）
    

---

## 一、 云端 AI 的潜在风险与本地 AI 的必要性

**[00:00在新窗口中打开](http://www.youtube.com/watch?v=7qIfFVb06bc&t=0)** 上周，世界上最强大的 AI 模型之一在半夜被突然关闭了——不是停用，也不是限流，而是直接关闭。对于许多依赖该模型的公司来说，前几天还在正常使用，过完周末就彻底无法访问了，而你对此无能为力。

**[00:18在新窗口中打开](http://www.youtube.com/watch?v=7qIfFVb06bc&t=18)** 这就是没有人告诉你的关于**云端 AI** 的真相：**你并不真正拥有这种能力，你只是在租用它。** 房东随时可以换掉门锁。

在这视频中，我将展示另一种选择：使用 **Hermes Desktop** 和 **Ollama** 在你自己的机器上运行完全本地化的 AI Agent。没有任何供应商能够对其进行限流、降级或直接下架。

---

## 二、 软件下载与本地环境配置

要搭建这个本地 AI 代理，你需要两款软件：

### 1. 下载并安装 Ollama

- **[01:32在新窗口中打开](http://www.youtube.com/watch?v=7qIfFVb06bc&t=92)** 访问 [ollama.com](https://ollama.com/) 下载适合你系统的版本（视频中以 Windows 平台为例）。
    
- 下载完成后，运行安装程序进行安装。
    

### 2. 下载并配置 Hermes Agent

- **[01:44在新窗口中打开](http://www.youtube.com/watch?v=7qIfFVb06bc&t=104)** Hermes Agent 是目前最受欢迎的云端 AI 桌面客户端替代品之一。
    
- 启动 Hermes Agent 后，先不要急着连接，需要先通过 Ollama 下载模型。
    

### 3. 下载模型并调整 Context（上下文）设置

- **[02:12在新窗口中打开](http://www.youtube.com/watch?v=7qIfFVb06bc&t=132)** 在 Ollama 中选择离线模型（视频中选择了 **Gemma 4**）。通过在聊天框中输入测试文本（如 "test"）来触发模型的下载。
    
- **[02:43在新窗口中打开](http://www.youtube.com/watch?v=7qIfFVb06bc&t=163)** **关键步骤：** 进入设置，将 **Context Layer（上下文层）更改为 64K**。
    
    > **注意：** Hermes Desktop Agent 会检查可用的上下文大小。如果小于 64K，系统会报错。
    

### 4. 将 Hermes 连接到本地 Ollama

- **[02:56在新窗口中打开](http://www.youtube.com/watch?v=7qIfFVb06bc&t=176)** 在 Hermes Agent 中选择“稍后选择供应商”（Choose provider later），进入设置，滚动到最下方找到 **Custom Endpoint（自定义端点）**。
    
- 输入本地 Ollama 的默认 URL（通常为 Open AI 兼容的本地 API 端口），点击 **Connect（连接）**。
    
- 连接成功后，右下角会显示 `Gemma latest (medium effort)`，此时本地环境已完全搭建完毕。
    

---

## 三、 本地 AI 性能实测与对比

**[03:44在新窗口中打开](http://www.youtube.com/watch?v=7qIfFVb06bc&t=224)** 接下来，主讲人将本地运行的 Hermes Desktop（左侧）与云端的 Co-work 进行了横向对比，两边输入完全相同的 Prompt（提示词：根据初次沟通的笔记生成一份假想机构的商业提案）。

### 1. 硬件负载与生成速度

- **[04:20在新窗口中打开](http://www.youtube.com/watch?v=7qIfFVb06bc&t=260)** 视频展示了运行期间的 GPU 资源监视器。主讲人使用的是一张 **12 GB 显存的 RTX 3070 显卡**（普通游戏显卡）。
    
- 在同时进行 OBS 录屏、音频转录和运行 Ollama 的情况下，专用 GPU 显存占用了 **10.3 GB / 12 GB**。
    
- 令人惊喜的是，本地模型的文档生成速度非常快，表现令人满意。
    

### 2. 工具调用与本地开源的局限性

- **[05:00在新窗口中打开](http://www.youtube.com/watch?v=7qIfFVb06bc&t=300)** 当要求本地模型直接“生成文件（如 .docx）”时，本地模型出现了拒绝或无法调用的情况。
    
- **对比：** 云端 Co-work 可以无缝加载各种 Skill（技能插件），并自动生成带有颜色、精美布局和表格的 Word 文档。
    
- **结论：** 虽然 Gemma 4 支持工具调用（Tool Calling），但要在本地完美整合 Python 的 `docx` 等依赖包，需要更复杂的配置。开源本地 AI 很难像云端开箱即用的产品那样做到面面俱到。
    

---

## 四、 本地 AI 的核心优势、成本与安全考量

### 1. 真的能省钱吗？

- **[06:32在新窗口中打开](http://www.youtube.com/watch?v=7qIfFVb06bc&t=392)** 很多人为了省钱而选择本地 AI。虽然一块 12GB 的显卡只需要 300 到 400 美元，普通电脑就能带得动，硬件门槛并不高。
    
- 但你需要算入**隐形成本**：环境搭建、后期维护以及管理这套系统所花费的时间。
    

### 2. 能力上的客观差距

- **[07:02在新窗口中打开](http://www.youtube.com/watch?v=7qIfFVb06bc&t=422)** 必须承认，任何在本地运行的模型，在绝对能力上都无法与云端的顶级模型（如 Fable 5 或 Opus 4.8）相提并论。开源模型尚未完全赶上，且本地硬件也无法支撑拥有数千亿参数的超大模型。
    

### 3. 本地 AI 的适用场景

本地 AI 胜在**控制权**和**业务连续性**。

- **高保密需求：** 绝对不能流出大楼的客户隐私数据或医疗数据。
    
- **研究与网络爬虫：** 许多社区用户在本地运行 Research Agent，在全网抓取信息。因为本地运行几乎只需要支付电费，完全没有 API 调用成本。
    

### 4. 安全与治理风险

- **[07:54在新窗口中打开](http://www.youtube.com/watch?v=7qIfFVb06bc&t=474)** **本地并不等同于绝对安全。** Hermes 可以真正访问你的本地机器并运行本地代码。
    
- **供应链攻击风险：** 这是一个开源仓库，如果有人向开源代码库中提交了恶意代码，它可能会在不知不觉中更新并运行在你的本地机器上。相比之下，像 Anthropic 这样的云端大厂在代码审计和内部合规上要严格得多。
    

---

## 五、 总结建议

**[08:33在新窗口中打开](http://www.youtube.com/watch?v=7qIfFVb06bc&t=513)** 对于绝大多数日常工作而言，托管的云端 AI 工具成本更低、能力更强、更易于管理。你应该接受“租用能力”的潜在风险并使用它。

但是，对于那一小部分**绝对不能离开本地、或者绝对无法承受停机风险**的核心业务，你可以像视频中这样，在本地电脑上部署一个属于自己的 AI Agent。

---