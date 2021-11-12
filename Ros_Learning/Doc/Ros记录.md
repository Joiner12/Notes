# ROS

## 1.Linux

### 1.1 Basic Syntax

```bash
#0x01 
$ echo
```

https://linux.cn/article-3948-1.html

```bash
#0x02
$ source
```

 https://www.cnblogs.com/pcat/p/5467188.html

3.'~' vs '/'

https://blog.csdn.net/lq_kl/article/details/81056241



## 2.Ros

### 2.1 rosdep init failed

1.ROS:sudo rosdep init出错常规方法都无效后解决办法记录

https://zhuanlan.zhihu.com/p/77483614

2.换源 https://blog.csdn.net/zhangmeimei_pku/article/details/79597951

### 2.2 ros安装卸载

1.kinetic安装 https://www.cnblogs.com/liu-fa/p/5779206.html

2.ros卸载 https://www.cnblogs.com/long5683/p/10260821.html



## 3.Tutorials

1.Tutorial

https://zhuanlan.zhihu.com/p/26007106

2.ros Chinese tutorial 

http://wiki.ros.org/cn/ROS/Tutorials

https://www.guyuehome.com/2500

3.Linux

http://www.ee.surrey.ac.uk/Teaching/Unix/



## 4.Vim

1.reference manual 

https://github.com/yianwillis/vimcdoc/releases



## 5.What Can Do

1.dacing dog

2.姿态识别

## 6.A Gentle Introduction to Ros

### 6.1 Getting started

在深入了解如何编写使用 ROS 的软件的细节之前，让 ROS 启动并运行并了解 ROS 使用的一些基本思想是很有价值的。

#### installing ROS

[wiki.ros.org/ROS/Installation](http://wiki.ros.org/ROS/Installation)

[indigo/Installation/Ubuntu - ROS Wiki](http://wiki.ros.org/indigo/Installation/Ubuntu)

#### Configuring your account

#### A minimal example using turtlesim

小海龟，在三个独立的终端中，执行这三个命令： 

```powershell
$ roscore
$ rosrun turtlesim turtlesim_node
$ rosrun turtlesim turtle_teleop_key
```

### 6.2 Packages

ROS 中的软件以包的形式组织。 一个包可能包含 ROS 节点、一个与 ROS 无关的库、一个数据集、配置文件、第三方软件或任何其他逻辑上构成有用模块的东西。 这些软件包的目标是以易于使用的方式提供这种有用的功能，以便可以轻松地重用软件。 一般来说，ROS 包遵循“金发姑娘”原则：足够的功能是有用的，但不会太多以至于包是重量级的并且难以从其他软件中使用。 在示例中，我们使用了两个名为turtlesim_node 和turtle_teleop_key 的可执行文件，它们都是turtlesim 包的成员。 [Packages - ROS Wiki](http://wiki.ros.org/Packages)

列出和定位软件包您可以使用以下命令获取所有已安装 ROS 软件包的列表： 

```powershell
$ rospack list
```

每个包都由一个清单定义，该清单是一个名为 package.xml 的文件。 此文件定义了有关包的一些详细信息，包括其名称、版本、维护者和依赖项。 包含 package.xml 的目录称为包目录。 （在 事实上，这是一个 ROS 包的定义：任何 ROS 能找到的包含名为 package.xml 的文件的目录都是一个包目录。）这个目录存储了大部分包的文件。

要查找单个包的目录，请使用 rospack find 命令： 

```powershell
$ rospack find package-name
```

当然，有时您可能不知道（或不记得）完整的 您感兴趣的包的名称。在这些情况下，这很方便 rospack 支持包名的制表符补全。 

```powershell
$ rospack find package-name
```

要查看包目录中的文件，请使用这样的命令 :

```powershell
$ rosls package-name 
```

如果您想“转到”包目录，可以使用如下命令将当前目录更改为特定包： 

<img src="img.img">

使用rosls和roscd查看turtlesim使用的海龟图片。 eog 命令是“侏儒之眼”图像查看器。 



### 6.3 The master

ROS Master 为 ROS 系统中的其余节点提供命名和注册服务。 它跟踪主题和服务的发布者和订阅者。 Master 的作用是使各个 ROS 节点能够相互定位。 一旦这些节点相互定位，它们就会相互进行点对点通信。 Master 还提供参数服务器。 Master 最常使用 roscore 命令运行，该命令加载 ROS Master 以及其他基本组件。 [Master - ROS Wiki](http://wiki.ros.org/Master)

```powershell
$ roscore
```

roscore 不接受任何参数，也不需要配置 。您应该允许 master 在您使用 ROS 的整个时间内继续运行。 大多数 ROS 节点在启动时连接到主节点，如果稍后连接失败，则不会尝试重新连接。 因此，如果你停止roscore，此时运行的任何其他节点都将无法建立新的连接，即使你稍后重启roscore。 

### 6.4 Nodes

一旦你启动了 roscore，你就可以运行使用 ROS 的程序。 ROS 程序的运行实例称为节点(Node)。 [Nodes - ROS Wiki](http://wiki.ros.org/Nodes)

在turtlesim 示例中，我们创建了两个节点。 一个节点是一个名为turtlesim_node 的可执行文件的实例。 该节点负责创建turtlesim窗口并模拟海龟的运动。 第二个节点是一个名为turtle_teleop_key 的可执行文件的实例。 缩写teleop 是缩写形式 远程操作一词，指的是人类远程控制机器人的情况 通过给出直接的移动命令。 该节点等待箭头键被按下， 将该按键转换为移动命令，并将该命令发送到turtlesim- _node 节点。创建节点（也称为“运行 ROS 程序”）的基本命令是 rosrun。

```powershell
$ rosrun package-name executable-name
```

rosrun 有两个必需的参数。 第一个参数是包名。第二个参数只是一个名称 该包中的可执行文件。

ROS 提供了几种方法来获取有关在任何特定时间运行的节点的信息：

```powershell
$ rosnode list
>> /rosout
>> /telsop_turtle
>> /turtlesim
```

/rosout 节点是一个特殊的节点，由 roscore 自动启动。 它的目的有点类似于您可能使用的标准输出（即 std::cout） 在控制台程序中。 

您可以使用以下命令获取有关特定节点的一些信息：

```
rosnode info node-name
```

## 7.Web  Info

1. 创建工作区间 & 环境变量检查 [cn/ROS/Tutorials/InstallingandConfiguringROSEnvironment - ROS Wiki](http://wiki.ros.org/cn/ROS/Tutorials/InstallingandConfiguringROSEnvironment#A.2BUhte.2Bg-ROS.2BXeVPXHp6lfQ-)
2. [Linux下source命令详解 - 水车 - 博客园 (cnblogs.com)](https://www.cnblogs.com/shuiche/p/9436126.html)
3. [树莓派3B+学习笔记：11、查看硬件信息 - Z-z-z - 博客园 (cnblogs.com)](https://www.cnblogs.com/trilobita/p/10600945.html#:~:text=查看树莓派硬件信息     . 1、查看CPU信息.,cat%2Fproc%2Fcpuinfo. 查看最后三行. 如果只想查看最后三行，也可使用这个命令. tail-3%2Fproc%2Fcpuinfo. lscpu. 2、查看树莓派型号. cat%2Fproc%2Fdevice-tree%2Fmodel.)

## 8.缓存扩展Raspberry 4B

```shell
# 注意，移植到树莓派主控的话，【kcf_track】功能包需要替换，树莓派版的【kcf_track】功能包在与本文档在同一级目录下的文件夹【kcf_track\raspberry\kcf_track】。
# 同时2GB内存的【树莓派4B】，需要进行缓存扩展后才可以进行编译，否则会树莓派会卡死。扩展缓存命令：
sudo dd if=/dev/zero of=/swap bs=1M count=4096
sudo mkswap /swap
sudo chmod 600 /swap
sudo swapon -a /swap 
# 第一个命令执行需要8分钟
```

