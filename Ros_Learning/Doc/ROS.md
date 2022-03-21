# A Gentle Introduction to Ros



<div style="text-align:center;">
    <img src="https://gitee.com/RiskyJR/pic-bed/raw/master/20220110111619.png" style="zoom:20%;">
</div>



## 1.介绍

​	ROS 是一个开源的、用于机器人的元操作系统。 它提供包括硬件抽象、低级设备控制、常用功能的实现、进程之间的消息传递和包管理。 它还提供用于在多台计算机上获取、构建、编写和运行代码的工具和库。

## 2.开始

在深入了解如何编写使用 ROS 的软件的细节之前，让 ROS 启动并运行并了解 ROS 使用的一些基本思想是很有价值的。

### 2.1 ROS安装

[wiki.ros.org/ROS/Installation](http://wiki.ros.org/ROS/Installation)

[indigo/Installation/Ubuntu - ROS Wiki](http://wiki.ros.org/indigo/Installation/Ubuntu)

### 2.2 Configuring your account

### 2.3 A minimal example using turtlesim

小海龟，在三个独立的终端中，执行这三个命令： 

```powershell
$ roscore
$ rosrun turtlesim turtlesim_node
$ rosrun turtlesim turtle_teleop_key
```

### 2.4 功能包(Packages)

ROS 中的软件以包的形式组织。 一个包可能包含 ROS 节点、一个与 ROS 无关的库、一个数据集、配置文件、第三方软件或任何其他逻辑上构成有用模块的东西。 这些软件包的目标是以易于使用的方式提供这种有用的功能，以便可以轻松地重用软件。 一般来说，ROS 包遵循“金发姑娘”原则：足够的功能是有用的，但不会太多以至于包是重量级的并且难以从其他软件中使用。 在示例中，使用了两个名为turtlesim_node 和turtle_teleop_key 的可执行文件，它们都是turtlesim 包的成员。 [Packages - ROS Wiki](http://wiki.ros.org/Packages)

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



### The master

ROS Master 为 ROS 系统中的其余节点提供命名和注册服务。 它跟踪主题和服务的发布者和订阅者。 Master 的作用是使各个 ROS 节点能够相互定位。 一旦这些节点相互定位，它们就会相互进行点对点通信。 Master 还提供参数服务器。 Master 最常使用 roscore 命令运行，该命令加载 ROS Master 以及其他基本组件。 [Master - ROS Wiki](http://wiki.ros.org/Master)

```powershell
$ roscore
```

roscore 不接受任何参数，也不需要配置 。您应该允许 master 在您使用 ROS 的整个时间内继续运行。 大多数 ROS 节点在启动时连接到主节点，如果稍后连接失败，则不会尝试重新连接。 因此，如果你停止roscore，此时运行的任何其他节点都将无法建立新的连接，即使你稍后重启roscore。 

### Nodes

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

### topics and message

节点之间是如何实现信息交换的？

ROS节点用以通信的主要机制是发送信息，信息被命名为`话题(topics)` 。基本思想是：想要共享信息的节点将发布有关适当话题； 想要接收信息的节点将订阅它感兴趣的一个或多个话题。 `master` 负责确保发布者和订阅者可以找到彼此； 消息本身直接从发布者发送到订阅者。

#### 查看发布-订阅关系图

```bash
rqt_graph
```

<img src="https://gitee.com/RiskyJR/pic-bed/raw/master/20220315101031.png">

椭圆形：节点

连接线：话题

话题/turtle1/cmd_vel是由于/teleop_turtle发布，由/turtlesim订阅；

#### Message and message types

```bash
#1. 列出活动节点
rostopic list
# 2.消息回显 
rostopic echo topic-name
# 3.消息发送频率和带宽
rostopic hz topic-name
rostopic bw topic-name
```

#### Inspecting a topic

了解节点详细信息

```bash
rostopic info topic-name
```

#### Inspecting a message

检查消息类型

```bash
rosmsg show message-type-name
```

#### Publishing messages from the command line

大多数情况下，发布消息的工作是由专门的程序完成的。但是，有时会发现手动发布消息很有用。 

```bash
rostopic pub -r rate-in-hz topic-name message-type message-content
rostopic pub -r 1 /turtle1/cmd_vel geometry_msgs/Twist ’[0, 0, 0]’ ’[0, 0, 1]’
```

[ROS自定义msg类型及使用_张京林要加油的技术专栏-CSDN博客_ros 自定义msg](https://blog.csdn.net/u013453604/article/details/72903398)

## Writing Ros programs

### Creating a workspace and a package

**工作空间的概念**

<img src="https://gitee.com/RiskyJR/pic-bed/raw/master/20220315165104.png" style="zoom:50%">

---

**Creating a workspace and a package** 

```bash
# 创建工作空间&编译
$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/
$ catkin_make
```

**catkin_make**

catkin_make 命令是使用 catkin 工作空间的便捷工具。 第一次在工作区中运行，将在“src”文件夹中创建一个 CMakeLists.txt 链接。 

**Creating a package**

实际上，这个包创建命令并没有做太多的事情：它创建一个目录来保存包，并在该目录中创建两个配置文件：

package.xml

CMakeLists.txt

```bash
# 工作空间的src文件路径下运行
$ cd ~/catkin_ws/src
# 创建一个名字为beginner_tutorials 依赖库为 std_msgs rospy roscpp的功能包
# 标准语法:
# catkin_create_pkg <package_name> [depend1] [depend2] [depend3]
$ catkin_create_pkg beginner_tutorials std_msgs rospy roscpp

```

**Compiling the Hello program**  

- Declaring dependencies

需要声明依赖的其他包。 对于 C++ 程序，需要这一步主要是为了确保 catkin 为 C++ 编译器提供适当的标志来定位它需要的头文件和库。 



```cmake
# CmakeLists.txt
# 依赖包
find_package(catkin REQUIRED COMPONENTS package-names)
# package.xml
# 使用 build_depend 和 run_depend 元素在包清单（package.xml）中列出依赖项
# 编译依赖项
<build_depend>package-name</build_depend>
# 运行依赖项
<run_depend>package-name</run_depend>

```

- Declaring an executable  

  接下来，需要在 CMakeLists.txt 中添加两行来声明想要创建的可执行文件。

```cmake
add_executable(executable-name source-files)
target_link_libraries(executable-name ${catkin_LIBRARIES})
```

第一行声明了想要的可执行文件的名称，以及应该组合成该可执行文件的源文件列表。 如果有多个源文件，在此处列出所有源文件，并用空格分隔。 第二行告诉 CMake 在链接这个可执行文件时使用适当的库标志（由上面的 find_package 行定义）。 如果功能包包含多个可执行文件，需要为每个拥有的可执行的文件复制并修改这两行。 

- Building the workspace  

  在workspace目录下编译多个功能包；

- Sourcing setup.bash   

  这个自动生成的脚本设置了几个环境变量，使 ROS 能够找到您的包及其新生成的可执行文件。 

```bash
source devel/setup.bash
```

### Executing the hello program 

```bash
# 启动master节点
roscore
# 运行节点
rosrun [package_name] [node_name]
```



1. <D:\ROS\大车ROS机器人附送资料_2021.06.04\2.ROS小车视频教程\2.ROS基础干货视频教程\1.工作空间与功能包\ROS_工作空间与功能包.pdf>
2. [catkin/Tutorials/create_a_workspace - ROS Wiki](http://wiki.ros.org/catkin/Tutorials/create_a_workspace)
3. [ROS/Tutorials/CreatingPackage - ROS Wiki](http://wiki.ros.org/ROS/Tutorials/CreatingPackage)
4. [roscpp/Overview/Initialization and Shutdown - ROS Wiki](http://wiki.ros.org/roscpp/Overview/Initialization and Shutdown)
5. [ROS/Tutorials/BuildingPackages - ROS Wiki](http://wiki.ros.org/ROS/Tutorials/BuildingPackages)
6. [ROS 工作空间、package 及 catkin 编译系统 - 简书 (jianshu.com)](https://www.jianshu.com/p/8b8029e93f32)
7. [ROS development with Visual Studio Code – Erdal's blog (erdalpekel.de)](https://erdalpekel.de/?p=157)

### A publisher program  

Publishing messages 

- Including the message type declaration  

  每个 ROS 主题都与一个消息类型相关联。 每个消息类型都有一个对应的 C++ 头文件。 需要为程序中使用的每种消息类型#include此标头，代码如下：

  ```c++
  include <package_name/type_name.h> 
  ```

  `Note:`包名称应该是包含消息类型的包的名称，而不是（必须）当前功能包的名称。 

- Creating a publisher object   

  实际发布消息的工作是由一个 ros::Publisher 类的对象完成，代码如下：

  ```c++
  ros::Publisher pub = node_handle.advertise<message_type>(topic_name, queue_size);
  ```

  topic_name 是一个字符串，其中包含我们要发布的主题的名称。 它应该与 rostopic list 或 rqt_graph 显示的主题名称匹配，但（通常）没有前导斜杠 (/)。 我们去掉前导斜杠，使主题名称成为相对名称； 第 5 章解释了相对名称的机制和用途。 在示例中，主题名为“turtle1/cmd_vel”。 

  广播的最后一个参数是一个整数，表示此发布者的消息队列的大小。 在大多数情况下，一个相当大的值（例如 1000）是合适的。 如果程序快速发布的消息超出队列可以容纳的数量，则最旧的未发送消息将被丢弃。 

- Creating and filling in the message object   

  接下来，我们创建消息对象本身。 我们在创建 ros::Publisher 对象时已经引用了消息类。 对象 该类中的每个底层消息类型中的每个字段都有一个可公开访问的数据成员。

- Publishing the message

  ...

- Formatting the output 

  ROS_INFO_STREAM 格式化输出；

