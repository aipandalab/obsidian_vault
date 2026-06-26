---
number headings: auto, first-level 1, max 6, 1.1
---
> [!info] 本章概览
> - 深入理解Python语言
> - Python蟒蛇绘制
> - 模块1:turtle库使用
> - turtle程序语法元素分析
> ---
> 方法论：Python语言及海龟绘图
> 
> 实践能力：初步学会使用Python绘制简单图形


> [!note] 第1单元
>  - **计算机技术的演进**
>  - **编程语言的多样初心**
>  - **Python语言的特点**
>  - **“超级语言”的诞生**

# 1 计算机技术的演进
	1946-1981 计算机系统结构时代 计算能力问题
	1981-2008 网络与视窗时代 人机、机机交互问题
	2008-2016 复杂信息系统时代 数据问题
	2016年- 人工智能时代 类人智能的问题
# 2 编程语言的多样初心
	编程语言也是一个江湖，目前出现过的编程语言超过600种
	
![image.png](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504211757595.png)

	- C语言：指针、内存、数据类型，本质：理解计算机系统结构，目标：程序性能更高，适合计算机专业人员做底层系统开发
	- Java语言：诞生于网络与视窗时代，面向对象降低复杂度，并实现跨平台，本质：理解主体与客体关系，适合软件类专业人员使用
	- C++语言：对象、多态、继承 本质：理解主体与客体关系，适合：计算机专业人员进行大规模程序的编写，比如：操作系统
	- VB语言：对象、控件，本质：理解人机交互逻辑，适合桌面应用的开发
	- Python语言：编程逻辑、第三方库，本质：理解问题求解，适合：所有专业解决各类问题
# 3 Python语言的特点
	通用语言、脚本语言、开源语言、跨平台语言、多模型语言
	其中：通用性是其最大的特点
	- 强制可读性
	- 较少的底层语法元素
	- 多种编程方式
	- 支持各种字符集
	- 语法简洁，不到C代码量的10%，编写效率10倍
	- 超过13万的第三方库
	- 完整的计算生态，避免重复造轮子
	- 开放共享
	- 跨平台

	人生苦短，我学Python
	Python归Python，C归C
	C编写的程序作为第三方库的方式提供Python调用

	Python是最高产的程序设计语言
	掌握抽象并求解计算问题综合能力的语言
	了解产业界解决复杂计算问题方法的语言
	享受利用编程将创新变为实现乐趣的语言

	工具决定思维：关注工具变革的力量，使用Python解决问题，将改变您解决问题的思维方式
![image.png|500](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504211823525.png)
# 4 “超级语言”的诞生
## 4.1 编程语言的种类
---
### 4.1.1 机器语言
	一种二进制语言，直接使用二进制代码表达指令
	计算机硬件CPU可以直接执行，与具体CPU型号有关
### 4.1.2 汇编语言
	- —种将二进制代码直接对应助记符的编程语言
	- 汇编语言与CPU型号有关，程序不通用，需要汇编器转换
### 4.1.3 高级语言
	- 更接近自然语言，同时更容易描述计算问题
	- 高级语言代码与具体CPU型号无关，编译后运行
### 4.1.4 超级语言
	粘性整合己有程序，具备庞大计算生态
	- 具有庞大计算生态，可以很容易利用已有代码功能
	- 编程恩维不再是刀耕火种 ，而是集成开发
	Python语言拥有最庞大的计算生态，所以是目前唯一的超级语言，未来的前景无法估量

> [!success] 第1单元小结：
> - ﻿计算机系统结构时代到人工智能时代的演进路线
> - 五种编程语言的初心和历史使命
> - Python语言的通用性、简洁性和生态性
> - Python是以计算生态为标志的"超级语言”

> [!note] 第2单元
>  - **用程序绘制一条蟒蛇**
>  - **turtle库的使用**
>  - **绘制玫瑰花送给TA**

# 5 实例2：Python蟒蛇绘制
## 5.1 设计蟒蛇的基本形状
![image.png|440](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504212202558.png)

## 5.2 编写代码
```Python
# PythonDraw.py  
import turtle  
  
turtle.setup(650, 350, 200, 200)  
turtle.penup()  
turtle.fd(-250)  
turtle.pendown()  
turtle.pensize(25)  
turtle.pencolor("purple")  
turtle.seth(-40)  
for i in range(4):  
    turtle.circle(40, 80)  
    turtle.circle(-40, 80)  
turtle.circle(40, 80 / 2)  
turtle.fd(40)  
turtle.circle(16, 180)  
turtle.fd(40 * 2 / 3)  
turtle.done()
```

## 5.3 举一反三
	- Python蟒蛇绘制问题是各类图像绘制问题的代表
	- 之后就可以绘制：圆形绘制、五角星绘制、国旗绘制、机器猫绘制…
	- 掌握绘制一条线的方法，你就可以绘制整个世界

# 6 turtle库的使用

## 6.1 标准库
	Pythont算生态 二标准库 ＋ 第三方库
	- 标准库：随解释器直接安装到操作系统中的功能模块
	- 第三方库：需要经过额外安装才能使用的功能模块
	- Library(库)、Package(包)、Module(模块)，统称:模块
## 6.2 turtle库基本介绍
	turtle(海龟)库是turtle绘图体系的Python实现
	- turtle绘图体系：1969年诞生，主要用于程序设计入门
	- Python语言的标准库之一
	- 入门级的图形绘制函数库
## 6.3 turtle绘图窗体布局
![image.png](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504220044108.png)

	设置窗体大小及位置：
	turtle.setup(width, height, start, starty)
	
![image.png|540](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504220047577.png)

## 6.4 turtle空间坐标体系
### 6.4.1 绝对坐标
![image.png|560](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504220049485.png)
![image.png](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504220052059.png)

### 6.4.2 海龟坐标
![image.png](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504220054972.png)
	fd：前进，bk：后退，circle：弧形
## 6.5 turtle角度坐标体系
### 6.5.1 绝对角度
![image.png](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504220056405.png)
	turtle.seth(angle)：只改变头部的方向
### 6.5.2 海龟角度

![image.png](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504221140706.png)
```Python
import turtle  
  
turtle.setup(800, 600)  
turtle.left(45)  
turtle.fd(150)  
turtle.right(135)  
turtle.fd(300)  
turtle.left(135)  
turtle.fd(150)  
turtle.done()
```

![image.png|158](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504221206278.png)

## 6.6 RGB色彩体系

![image.png](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504221208765.png)
![image.png](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504221242219.png)
	turtle库默认采用RGB小数值定义颜色，可切换为整数值模式，如下：
	turtle.colormode (mode)，其中mode的取值为：
	- ﻿1.0：RGB小数值模式
	- 255： RGB整数值模式

> [!success] 第2单元小结：
> - ﻿turtle库的海龟绘图法
> - turtle.setup0调整绘图窗体在电脑屏幕中的布局
> - 画布上以中心为原点的空间坐标系：绝对坐标&海龟坐标
> - 画布上以空间x轴为0度的角度坐标系：绝对角度&海龟角度
> - RGB色彩体系，整数值＆小数值，色彩模式切换

> [!note] 第3单元
>  - **库引用与import**
>  - **turtle画笔控制函数**
>  - **turtle运动控制函数**
>  - **turtle方向控制函数**
>  - **- for in 循环语句**
>  - **- "Python蟒蛇绘制"代码分析**

# 7 库引用与import
	扩充Python程序功能的方式
	- 使用import保留宇完成，采用<a>.<b>0编码风格
	- 引用语法：import <库名＞
	- 调用语法：＜库名＞.<函数名＞（＜函数参数＞）

	更多用法1：
	使用from和import保留字共同完成
	引用方法1:from <库名＞import <函数名＞
	引用方法2:from<库名＞import *
	调用方法：＜函数名＞（<函数参数>）

```Python
from turtle import *  
  
setup(650, 350, 200, 200)  
penup()  
fd(-250)  
pendown()  
pensize(25)  
pencolor("purple")  
seth(-40)  
for i in range(4):  
    circle(40, 80)  
    circle(-40, 80)  
circle(40, 80 / 2)  
fd(40)  
circle(16, 180)  
fd(40 * 2 / 3)  
done()
```

	两种方法对比：
	- 采用import <库名>的方式不会出现函数重名的问题，第二种存在重名问题

	更多用法2：
	使用import和as保留字共同配合，给调用的外部库关联一个更短、更适合自己的名字
	import <库名＞as<库别名＞
	＜库别名＞.<函数名＞（<函数参数＞）

```Python
import turtle as t  
  
t.setup(650, 350, 200, 200)  
t.penup()  
t.fd(-250)  
t.pendown()  
t.pensize(25)  
t.pencolor("purple")  
t.seth(-40)  
for i in range(4):  
    t.circle(40, 80)  
    t.circle(-40, 80)  
t.circle(40, 80 / 2)  
t.fd(40)  
t.circle(16, 180)  
t.fd(40 * 2 / 3)  
t.done()
```

# 8 turtle画笔控制函数
	画笔操作后一直有效，一般成对出现
	- turtle.penup() 别名：turtle.pu()，抬起画笔，海龟在飞行，不在画布上出现图案
	- turtle.pendown() 别名 turtle.pd()，落下画笔，海龟在爬行，画布上将出现图案
	- turtle.pensize(width） 别名 turtle width(width)，画笔宽度，海龟的腰围
	- turtle.pencolor(color) color为颜色字符串或RGB值，画笔颜色，海龟提着颜料桶
	
	pencolor(color)的color参数可以有三种形式：
	- ﻿颜色字符串：turtle.pencolor(”purplem")
	- RGB的小数值 ：turtle.pencolor(0.63, 0.13， 0.94)
	- RGB的元组值：turtle.pencolor((0.63,0.13,0.94))

# 9 turtle运动控制函数
## 9.1 控制海龟走直线：
	- turtle.forward(d）别名：turtle.fd(d)，作用：向前行进，海龟走直线
	- d：行进距离，单位是像素，可以为负数，表示海龟倒退方式行进
## 9.2 控制海龟走曲线：
	- turtle.circle(r, extent=None)，根据半径r绘制extent角度的弧形
	- r：默认圆心在海龟左侧r距离的位置
	- extent:绘制角度，默认是360度整圆

![image.png|440](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504221341966.png)

![image.png|440](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504221342335.png)

	在海龟右侧100像素位置为圆心，爬行90度
	
# 10 turtle方向控制函数
## 10.1 绝对角度
	-turtle.setheading(angle） 别名 turtle.seth(angle)
	- ﻿angle：海龟面向的绝对角度

![image.png](https://panda-ai-316.oss-cn-chengdu.aliyuncs.com/obsidian/202504221511993.png)

## 10.2 海龟角度
	- ﻿turtle.left(angle)  海龟向左转angle度数
	- turtle.right(angle)  海龟向右转angle度数

# 11 for in 循环语句
```
for<变量＞in range（＜参数＞）:

＜被循环执行的语句＞
```
## 11.1 range()函数
	产生循环计数序列
	- range(N)  产生 0到N-1的整数序列，共N个
	- range(M,N)  产生M到N-1的整数序列，共N-M个

# 12 "Python蟒蛇绘制"代码分析
	暂略

> [!success] 第3单元小结：
> - ﻿库引用：import. from.import. import..as..
> - ﻿penup(). pendow(). pensize(), pencolor()
> - ﻿fd(). circle(). seth()
> - 循环语句：for和in、range0函数

# 13 练习实践
## 13.1 练习题
	5道编程题
## 13.2 作业
	15道单选题


