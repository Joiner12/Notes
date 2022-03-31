# A Gentle Introduction to Ros


## 1.介绍:selfie:

​	ROS 是一个开源的、用于机器人的元操作系统。 它提供包括硬件抽象、低级设备控制、常用功能的实现、进程之间的消息传递和包管理。 它还提供用于在多台计算机上获取、构建、编写和运行代码的工具和库。

## 2.开始

在深入了解如何编写使用 ROS 的软件的细节之前，让 ROS 启动并运行并了解 ROS 使用的一些基本思想是很有价值的。

### 2.1 ROS安装

1. 鱼香ROS—一行代码解决人生困惑

   ```bash
   wget http://fishros.com/install -O fishros && . fishros
   ```

   [一行代码解决烦恼 (fishros.com)](https://fishros.com/docs/page/#/tools/install-ros/一行代码安装完成ROS)

2. 官网安装

   [1] [wiki.ros.org/ROS/Installation](http://wiki.ros.org/ROS/Installation)

   [2] [indigo/Installation/Ubuntu - ROS Wiki](http://wiki.ros.org/indigo/Installation/Ubuntu)

3. 检查Ubuntu版本

   ```bash
   lsb_release -a
   # No LSB modules are available.
   # Distributor ID:	Ubuntu
   # Description:	Ubuntu 18.04.6 LTS
   # Release:	18.04
   # Codename:	bionic
   ```

4. 安装turtlesim功能包

   ```bash
   $ sudo apt-get install ros-indigo-turtlesim
   ```

### 2.2 运行turtle——最小实例

小海龟，在三个独立的终端中，执行这三个命令： 

```powershell
$ roscore
$ rosrun turtlesim turtlesim_node
$ rosrun turtlesim turtle_teleop_key
```

### 2.3 功能包(Packages)

ROS 中的软件以包的形式组织。 一个包可能包含 ROS 节点、一个与 ROS 无关的库、一个数据集、配置文件、第三方软件或任何其他逻辑上构成有用模块的东西。 这些软件包的目标是以易于使用的方式提供这种有用的功能，以便可以轻松地重用软件。 一般来说，ROS 包遵循“金发姑娘”原则：足够的功能是有用的，但不会太多以至于包是重量级的并且难以从其他软件中使用。 在示例中，使用了两个名为turtlesim_node 和turtle_teleop_key 的可执行文件，它们都是turtlesim 包的成员。 [Packages - ROS Wiki](http://wiki.ros.org/Packages)

列出和定位软件包您可以使用以下命令获取所有已安装 ROS 软件包的列表： 

```powershell
$ rospack list
```

每个包都由一个清单定义，该清单是一个名为 *package.xml* 的文件。 此文件定义了有关包的一些详细信息，包括其名称、版本、维护者和依赖项。 包含 *package.xml* 的目录称为包目录。（事实上，这是一个 ROS 包的定义：任何 ROS 能找到的包含名为 *package.xml* 的文件的目录都是一个**包目录**。）这个目录存储了大部分包的文件。

要查找单个包的目录，使用 rospack find 命令： 

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

如果想“转到”包目录，可以使用如下命令将当前目录更改为特定包： 

```bash
$ # 跳转到功能包指定子文件夹
$ roscd package-name/directory 
$ # 或者直接跳转功能包文件夹
$ roscd package-name
```

### 2.4 master

ROS 中Master 为 ROS 系统中的其余节点提供命名和注册服务。 它跟踪主题和服务的发布者和订阅者。 Master 的作用是使各个 ROS 节点能够相互定位。 一旦这些节点相互定位，它们就会相互进行点对点通信。 Master 还提供参数服务器。 Master 最常使用 roscore 命令运行，该命令加载 ROS Master 以及其他基本组件。 [Master - ROS Wiki](http://wiki.ros.org/Master)

```powershell
$ roscore
```

roscore 不接受任何参数，也不需要配置 。您应该允许 master 在您使用 ROS 的整个时间内继续运行。 大多数 ROS 节点在启动时连接到主节点，如果稍后连接失败，则不会尝试重新连接。 因此，如果你停止roscore，此时运行的任何其他节点都将无法建立新的连接，即使你稍后重启roscore。 

### 2.5 节点(Nodes)

一旦你启动了 roscore，你就可以运行使用 ROS 的程序。 ROS 程序的运行实例称为节点(Node)。 [Nodes - ROS Wiki](http://wiki.ros.org/Nodes)

在turtlesim 示例中，我们创建了两个节点。 一个节点是一个名为turtlesim_node 的可执行文件的实例。 该节点负责创建turtlesim窗口并模拟海龟的运动。 第二个节点是一个名为turtle_teleop_key 的可执行文件的实例。通过给出直接的移动命令。 该节点等待箭头键被按下， 将该按键转换为移动命令，并将该命令发送到turtlesim_node节点。创建节点（也称为“运行 ROS 程序”）的基本命令是 rosrun。

```powershell
$ rosrun package-name executable-name
```

rosrun 有两个必需的参数。 第一个参数是功能包名。第二个参数只是一个名称为该功能包中的可执行文件。

ROS 提供了几种方法来获取有关在任何特定时间运行的节点的信息：

- 列出活动节点

  ```bash
  $ rosnode list
  >> /rosout
  >> /telsop_turtle
  >> /turtlesim
  ```

  /rosout 节点是一个特殊的节点，由 roscore自动启动。它的目的有点类似于在控制台程序中使用的标准输出（即 std::cout） 。 

- 检查节点信息

  获取有关特定节点的一些信息

  ```bash
  $ rosnode info node-name
  ```

- 停止节点

  ```bash
  $ rosnode kill node-name
  ```

  与停止和重启master不同，停止和重启一个节点通常不会对其他节点产生重大影响； 即使对于正在交换消息的节点，这些连接也会在节点被终止时被丢弃，并在节点重新启动时重新建立。 

### 2.6 话题和消息(topics and message)

节点之间是如何实现信息交换的？

ROS节点用以通信的主要机制是发送信息，信息被命名为`话题(topics)` 。基本思想是：想要共享信息的节点将发布有关适当话题； 想要接收信息的节点将订阅它感兴趣的一个或多个话题。 `master` 负责确保发布者和订阅者可以找到彼此； 消息本身直接从发布者发送到订阅者。

#### 2.6.1 查看发布-订阅关系图

```bash
$ rqt_graph
```

<img src="D:\pic-bed\20220315101031.png">

椭圆形：节点

连接线：话题

话题/turtle1/cmd_vel是由于/teleop_turtle发布，由/turtlesim订阅；

#### 2.6.2 消息和消息类型(Message and message types)

```bash
#1. 列出活动节点
rostopic list
# 2.消息回显 
rostopic echo topic-name
# 3.消息发送频率和带宽
rostopic hz topic-name
rostopic bw topic-name
```

#### 2.6.3 检查消息类型(Inspecting a message)

```bash
$ rosmsg show message-type-name
```

#### 2.6.4 命令行发布消息

大多数情况下，发布消息的工作是由专门的程序完成的。但是，有时会发现手动发布消息很有用。 

```bash
rostopic pub -r rate-in-hz topic-name message-type message-content
rostopic pub -r 1 /turtle1/cmd_vel geometry_msgs/Twist ’[0, 0, 0]’ ’[0, 0, 1]’
```

[ROS自定义msg类型及使用_张京林要加油的技术专栏-CSDN博客_ros 自定义msg](https://blog.csdn.net/u013453604/article/details/72903398)

## 3.ROS 编程

### 3.1 创建工作空间和功能包

**工作空间的概念**

ROS中的所有软件都是以功能包的形式组织的，工作空间用来组织这些功能包。工作空间文件结构如下：

<img src="D:\pic-bed\20220315165104.png" style="zoom:50%">

---

- **创建工作空间** 

  ```bash
  # 创建工作空间&编译
  $ mkdir -p ~/catkin_ws/src
  $ cd ~/catkin_ws/
  $ catkin_make
  ```

  catkin_make 命令是使用 catkin 工作空间的便捷工具。 第一次在工作区中运行，将在"src"文件夹中创建一个 CMakeLists.txt 链接。 

  [catkin/Tutorials/create_a_workspace - ROS Wiki](http://wiki.ros.org/catkin/Tutorials/create_a_workspace)

- **创建功能包**

  创建功能包基本指令，它创建一个目录来保存功能包并在该目录中创建两个配置文件，*package.xml*，*CMakeLists.txt*。

  ```bash
  $ catkin_create_pkg package-name
  ```

  实例

  ```bash
  # 工作空间的src文件路径下运行
  $ cd ~/catkin_ws/src
  # 创建一个名字为beginner_tutorials 依赖库为 std_msgs rospy roscpp的功能包
  # 标准语法:
  # catkin_create_pkg <package_name> [depend1] [depend2] [depend3]
  $ catkin_create_pkg beginner_tutorials std_msgs rospy roscpp
  
  ```

### 3.2 Hello,ROS

1. **源码**

   在功能包下的"src"文件夹中创建一个hello.cpp文件。文件内容如下：

   ```cpp
   // this head define the ROS basic classes
   # include <ros/ros.h>
   int main(int argc,char **argv)
   {
       // initialize the ROS system
       ros::init(argc,argv,"hello_ros");
       // establish this program as a ROS node
       ros::NodeHandle nh;
       // console print
       ROS_INFO_STREAM("Hello ROS");
   }
   ```

2. **编译**

   ROS的编译是通过catkin完成的，编译过程包括四步：

   - 首先，需要声明程序依赖的其他包。 对于C++程序，这一步主要是为了确保 catkin 为 C++ 编译器提供适当的标志来定位它需要的头文件和库。 要列出依赖项，需要编辑包目录中的CMakeLists.txt。默认值为：

     ```makefile
     find_package(catkin REQUIRED)
     ```

     要添加其他依赖包，需要COMPONENTS 部分添加：

     ```makefile
     find_package(catkin REQUIRED COMPONENTS package-names)
     ```

     包清单 (package.xml) 中用 *build_depend* 和 *run_depend* 元素在列出依赖项： 

     ```xml
     <build_depend>package-name</build_depend>
     <run_depend>package-name</run_depend>
     ```

   - 声明可执行文件 

     在CMakeLists.txt中添加两行声明要创建的可执行文件。 一般形式是 :

     ```makefile
     add_executable(executable-name source-files)
     target_link_libraries(executable-name ${catkin_LIBRARIES})
     ```

     如果包含多个可执行文件，为每个可执行文件复制并修改这两行。

     实例：

     ```makefile
     add_executable(hello hello.cpp)
     target_link_libraries(hello ${catkin_LIBRARIES})
     ```

     

   - 编译工作空间

     使用catkin编译工作空间中所有的可执行文件，因为它旨在构建工作空间中的所有包，所以必须从工作空间目录运行此命令。

   - **Sourcing** setup.bash

     最后一步是执行一个名为 setup.bash 的脚本，该脚本由 catkin_make 在工作区的 devel 子目录中创建。运行的作用是自动生成的脚本设置了几个环境变量，使 ROS 能够找到包及其新生成的可执行文件。需要在每个终端执行一次，即使修改代码并使用 catkin_make 重新编译，但是修改文件夹结构需要重新source。

     ```bash
     $ source devel/setup.bash
     ```

3. **运行程序**

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

### 3.3 话题发布和订阅



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

### A subscriber program

- **Writing a callback function** 

  发布和订阅之间的一个重要区别是订阅者节点不知道消息何时到达。 为了处理这个问题，我们必须将任何响应传入消息的代码放在一个回调函数中，ROS 为每个到达的消息调用一次。

  **callback function**

  ```cpp
  void function_name(const package_name::type_name &msg) {
  . . .
  }
  ```

  *package_name* 和 *type_name* 与发布相同：它们指的是我们计划订阅的主题的消息类。 

- **Creating a subscriber object** 

  ```cpp
  //
  ros::Subscriber sub = node_handle.subscribe(topic_name,queue_size, pointer_to_callback_function);
  ```

- **Giving ROS control** 

  ```cpp
  // difference of spinOnce & spin
  ros::spinOnce();
  ros::spin();
  ```

- **Compiling and executing**

  

## Log messages



## Graph resource names

ROS 如何解析节点、主题、参数和服务的名称。 

### Global names

节点、主题、服务和参数统称为图资源(*Graph resource*)。 

它们被称为全局名称，因为它们在任何使用它们的地方都有意义。 这些名称具有清晰、明确的含义，无论它们是否被用作众多名称之一的论据 命令行工具或节点内部。 不需要额外的上下文信息来决定名称所指的资源。 

全局名称有几个部分：

```bash
/{namespace}/{namespace}/.../base_name
```

### Relative names

😀

### Private names

↕️↔️

### Anonymous names

🆘🆙🆚🈁

## Parameters

ROS提供了另外一种参数机制来从节点获取信息。思路是：由参数服务器(parameter service )来跟踪一系列值。因为参数必须由对其值感兴趣的节点主动查询，所以最适合不会随时间变化（很大）的配置信息 。

### Accessing parameters from the command line



- **Listing Parameters**

```bash
# 列出所有存在的参数
rosparam list
```

- **Querying parameters** 

  向参数服务器询问参数的值：

  ```bash
  rosparam get parameter_name
  ```

  检索命名空间中每个参数的值 ：

  ```bash
  rosparam get namespace
  ```

- **Setting parameters**

  ```bash
  rosparam set parameter_name parameter_value
  # 同时设置多个值
  rosparam set /duck_colors "huey: red
  dewey: blue
  louie: green
  webby: pink"
  ```

- **Creating and loading parameter files** 

  存储命名空间中的所有参数， 以 YAML 格式保存到文件中：

  ```bash
  rosparam dump filename namespace
  ```

  *dump* 的反面是 *load*，它从文件中读取参数并添加到参数服务器：

  ```bash
  rosparam load filename namespace
  ```

- **Setting the background color**

  例子：修改turtlesim中背景颜色，修改参数后颜色并不生效：

  ```bash
  # 启动ros
  roscore
  # 
  rosrun turtlesim  turtlesim_node
  # 修改参数
  rosparam set /background_b 255 
  # The explanation is that turtlesim_node only reads the values of these parameters when its /clear service is called
  rosservice call /service
  ```

  

### Accessing parameters from C++

```cpp
void ros::param::set(parameter_name, input_value);
bool ros::param::get(parameter_name, output_value);
```

在这两种情况下，参数名称都是字符串，可以是全局、相对或私有名称。 *set* 的输入值可以是 std::string、bool、int 或 double； get 的输出值应该是其中一种类型的变量（通过引用传递）。 如果值被成功读取，*get* 函数返回 true，如果存在则返回 false，通常表明请求的参数没有被赋值。

### Setting parameters in launch files

- **Setting parameters**

  设置参数（ relative name）的另一种非常常见的方法是在启动文件中进行。

  ```xml
  <param name="param-name" value="param-value" />
  <!-- e.g: -->
  <group ns="duck_colors">
  <param name="huey" value="red" />
  <param name="dewey" value="blue" />
  <param name="louie" value="green" />
  <param name="webby" value="pink" />
  </group>
  
  ```

- **Setting private parameters**

  将参数设置包含在一个节点中间；参数被视为该节点的私有名称。 

  ```xml
  <node>
  	<param name="param-name" value="param-value" />
  	. . .
  </node>
  ```

- **Reading parameters from a files**

  *launch file*还支持一次设置多个参数，等效于 *rosparam load*。

  ```xml
  <rosparam command="load" file="path-to-param-file" />
  ```

  此处列出的参数文件通常是由 rosparam dump 创建的。 与对特定文件的其他引用（一样，通常使用查找替换来指定相对于包目录的文件名： 

  ```xml
  <rosparam
  	command="load"
  	file="$(find package-name)/param-file"
  />
  ```

## Launch files

使用launch files一次配置和运行多个节点；

###  Using launch files

- **Executing launch files**

```ros
roslaunch package-name launch-file-name
```

关于 roslaunch 的一个重要事实（很容易忘记）是所有 启动文件中的节点大致同时启动。 因此，您无法确定 关于节点将自己初始化的顺序。 

- **Requesting verbosity**

  ```bash
  roslaunch -v package-name launch-file-name
  ```

- **Ending a launched session** 

  Ctrl-C

### Creating launch files

#### Where to place launch files

​	与所有其他 ROS 文件一样，每个启动文件都应与特定的包相关联。 通常的命名方法是以 *.launch* 结尾。 存储启动文件最简单的地方是直接在包目录中。在查找启动文件时，*roslaunch* 还会搜索每个包目录的子目录。 只要存储在包目录下即可，不论是首级文件夹还是在次级文件夹中。

####  Basic ingredients

最简单的启动文件由包含多个节点元素的根元素组成。

- **Launching nodes**

  like this:

  ```xml
  <!-- 隐式闭标签 -->
  <node
  pkg="package-name"
  type="executable-name"
  name="node-name"
  />
  
  <!-- 显示闭标签-->
  <node>
      pkg="package-name"
  	type="executable-name"
  	name="node-name"
  </node>
  
  ```

  *pkg* 和 *type* 属性标识应该运行哪个程序 ROS 来启动这个节点。 这些与 *rosrun* 的两个命令行参数相同，分别指定包名和可执行文件名。 *name* 属性为节点分配一个名称。 这会覆盖节点在调用 *ros::init* 时通常会分配给自己的任何名称。 

- **Finding node log files** 

  *roslaunch* 和 *running each* 之间的一个重要区别 单独使用 *rosrun* 的节点默认情况下，已启动节点的标准输出被重定向到日志文件，并且不会出现在控制台上。此日志文件的名称是： 

  ```bash
  ∼/.ros/log/run_id/node_name-number-stdout.log
  ```

- **Directing output to the console**

  ```bash
  output="screen"
  ```

  将单个节点的输出重定向到*console*。

  除了只影响单个节点的输出属性之外，我们还可以使用 *--screen* 命令行选项强制 roslaunch 显示其所有节点的输出：

  ```bash
  roslaunch --screen package-name launch-file-name
  ```

- **Requesting respawning**

  ```bash
  respawn="true"
  ```

  启动所有请求的节点后，roslaunch 监控 每个节点，跟踪哪些节点保持活动状态。 对于每个节点，我们可以通过使用 respawn 属性让 roslaunch 在它终止时重新启动它： 

- **Requiring nodes**

  ```bash
  required="true"
  ```

  兼容性，需求性检查。

  当所需节点终止时，roslaunch 通过终止所有其他活动节点并自行退出来做出响应。 这种行为可能很有用，例如，对于 (a) 非常重要的节点，如果它们失败，则应该放弃整个会话，并且 (b) 不能通过 respawn 属性优雅地重新启动。 该示例使用了 turtle_teleop_key 节点的 required 属性。 如果关闭远程操作节点运行的窗口，roslaunch 将杀死其他两个节点并退出。 

- **Launching nodes in their own windows** 

  ```bash
  launch-prefix="command-prefix"
  ```

  单独分配终端启动某个节点。

### Launching nodes inside a namespace

### Remapping names

### Other launch fifile elements

#### Including other files

要包含另一个启动文件的内容，包括其所有节点和参数，请使用 include 元素： 

```xml
<include file="path-to-launch-file" />
```

*file* 属性需要我们想要包含的文件的完整路径。 因为直接输入这些信息既麻烦又脆弱，大多数包含元素使用查找替换来搜索包，而不是显式命名目录：

```xml
<include file="$(find package-name)/launch-file-name" />
```

*include* 元素还支持将其内容推送到命名空间的 *ns（namespace）* 属性： 

```xml
<include file=". . . " ns="namespace" />
```

####  Launch arguments

为了帮助使启动文件可配置，*roslaunch* 支持启动参数，也称为*parameter*甚至 *args*，其功能有点像可执行程序中的局部变量 :

- **Declaring arguments**

  ```xml
  <arg name="arg-name" />
  ```

  

- **Assigning argument values** 

  启动文件中使用的每个参数都必须赋值。 有几种方法可以做到这一点。 您可以在 roslaunch 命令行上提供一个值：

  ```bash
  roslaunch package-name launch-file-name arg-name:=arg-value
  ```

  或者，您可以使用这两个之一提供一个值作为 arg 声明的一部分 句法:

  ```xml
  <arg name="arg-name" default="arg-value" />
  <arg name="arg-name" value="arg-value" />
  ```

  它们之间的唯一区别是命令行参数可以覆盖*default*值，但不能覆盖*value*的值； 

- **Accessing argument values** 

  一旦声明了一个参数并为其分配了一个值，您可以使用 arg 替换来使用它的值，如下所示：

  ```bash
  $(arg arg-name)
  ```

- **Sending argument values to included launch files**

  ```xml
  <include file="path-to-launch-file">
  <arg name="arg-name" value="arg-value"/>
  . . .
  </include>
  <arg name="arg-name" value="$(arg arg-name)" />
  ```



###  Creating groups

最后一个启动文件功能是 group 元素，它提供了一种在大型启动文件中组织节点的便捷方式。group 元素有两个用途： 

1. 组可以将多个节点推送到同一个命名空间中

   ```xml
   <group ns="namespace">
   . . .
   </group>
   ```

   

2. 组可以有条件地启用或禁用节点

   ```xml
   <!-- if -->
   <group if="0-or-1">
   . . .
   </group>
   <!-- unless -->
   <group unless="1-or-0">
   . . .
   </group>
   ```

## 服务(Services)

ROS系统中的一种通信机制，相比较于另外一种通信机制*message*有以下不同：

1. 服务调用是双向的(bi-directional)。 service中，一个节点向另一个节点发送信息并等待响应。 信息双向流动。 相反，message中当消息发布时，没有响应的概念，甚至不能保证有节点订阅了这些消息。
2. 服务调用实现点对点的通信。每个服务调用由一个节点发起，响应返回到同一节点。相反，每条消息都与一个可能有许多发布者和许多订阅者的主题相关联。 

除了上述之外，服务(service)和信息(message)基本相似。

### 服务概念(Terminology)

![image-20220324165236677](C:/Users/W-H/AppData/Roaming/Typora/typora-user-images/image-20220324165236677.png)

Services运行机制：客户端(*client*)节点发送请求(*request*)到服务器(*server*)节点，等待服务器节点回复。服务器接收到请求之后，对请求做出相应的动作后，发送响应(*response*)到客户端。

请求和响应数据的具体内容由**服务数据类型**决定，类似于决定消息内容的消息类型。类似于消息类型，服务数据类型由命名字段的集合定义。唯一不同的是，服务数据类型分为请求和相应两部分。

### 从命令行查找和调用服务

- **获取当前处于活动状态的服务列表 **

  ```bash
  rosservice list
  ```
  
- **查看某个特定节点提供的服务**

  ```bash
  rosnode info node-name
  ```
  
- **反向查询 ** **查找提供服务的节点 **

  ```bash
  rosservice node service-name
  ```
  
- **查找服务的数据类型** 

  ```bash
  rosservice info service-name
  ```

- **检查服务数据类型 ** 

  ```bash
  rossrv show service-data-type-name
  ```

- **从命令行调用服务** 

  ```bash
  rosservice call service-name request-content
  ```

实例1：

乌龟例程中的服务

```bash
# 启动ros
roscore
# 新开一个标签页 运行ros乌龟节点
rosrun turtlesim turtlesim_node
# 新开一个标签页 调用“/spawn”服务新生一只乌龟
# x:1 y:1 theta:1 name:"turtle2"
rosservice call /spawn 1 1 1 "lendo"
```

### A client program

从命令行调用服务对于探索和只需要偶尔做的事情很方便， 但是当然，能够从您的代码中调用服务会更有用。服务客户端的基本元素：

```cpp
#include <ros/ros.h>
#include <turtlesim/Spawn.h>

int main(int argc, char **argv) {
  ros::init(argc, argv, "spawn_tuetle");
  ros::NodeHandle nh;

  //为spawn服务创建客户端实例
  ros::ServiceClient spawnClient = nh.serviceClient<turtlesim::Spawn>("spawn");

  // 创建请求和响应实例
  turtlesim::Spawn::Request req;
  turtlesim::Spawn::Response resp;

  // 数据填充
  req.x = 1;
  req.y = 2;
  req.theta = 1;
  req.name = "whatthefuck";

  // 调用服务
  bool success = spawnClient.call(req, resp);
  if (success) {

    ROS_INFO_STREAM("fucl" << resp.name);
  } else {
    ROS_ERROR_STREAM("fuck u tommy");
  }
}
```



### A server program

```cpp
#include <geometry_msgs/Twist.h>
#include <ros/ros.h>
#include <std_srvs/Empty.h>

bool forward = true;
bool toggleForward(std_srvs::Empty::Request &req,
                   std_srvs::Empty::Request &resp) {
  forward = !forward;
  ROS_INFO_STREAM("CAONIMA " << (forward ? "forward" : "rotate") << "commands");
  return true;
}

int main(int argc, char **argv) {
  ros::init(argc, argv, "pubvel_toggle");
  ros::NodeHandle nh;

  // 注册服务器
  ros::ServiceServer server =
      nh.advertiseService("toggle_forward", &toggleForward);

  // 发布指令
  ros::Publisher pub =
      nh.advertise<geometry_msgs::Twist>("turtle1/cmd_vel", 1000);
  ros::Rate rate(2);
  while (ros::ok()) {
    geometry_msgs::Twist msg;
    msg.linear.x = forward ? 1 : 1;
    msg.linear.y = forward ? 0.0 : 1.0;
    pub.publish(msg);
    ros::spinOnce();
    rate.sleep();
  }
}
```



## Recording and replaying messages

使用 *rosbag*，我们可以将发布在一个或多个主题上的消息记录（*record*）到一个文件中，然后再回放(*replay*)这些消息 。

### Recording and replaying bag files

包文件(*bag file*)是指存储带时间戳(timestamp)的 ROS 消息的特殊格式文件。 *rosbag* 命令可用于记录和回放包文件。

- **Recording bag files**

  ```bash
  rosbag record -O filename.bag topic-names
  ```

  如果你不给文件名，*rosbag* 会根据当前的日期和时间为你选择一个。 此外，*rosbag* 记录还有一些其他选项可能有用。 

  - *-a* 您可以使用 `-a` 记录当前正在发布的每个主题的消息，而不是列出特定主题 。
  - *-j* 启用压缩

-  **Replaying bag files**

  ```bash
  rosbag play filename.bag
  ```

  

- **Inspecting bag files**

  ```bash
  rosbag info filename.bag
  ```

### Bags in launch files

除了我们已经看到的 rosbag 命令之外，ROS 还提供了名为 record 和 play 的可执行文件，它们是 rosbag 包的成员。 这些程序分别具有与 rosbag record 和 rosbag play 相同的功能并接受相同的命令行参数。 这意味着，一方面，可以使用 *rosrun* 实现录制和重放，如下所示：

```bash
rosrun rosbag record -O filename.bag topic-names
rosrun rosbag play filename.bag
```

更重要的是，通过包含适当的节点元素，这些执行操作可以作为启动文件的一部分。

```xml
<!-- a record node -->
<node
	pkg="rosbag"
	name="record"
	type="record"
	args="-O filename.bag topic-names"
/>
<!-- a play node -->
<node
	pkg="rosbag"
	name="play"
	type="play"
	args="filename.bag"
/>
```

## Conclusion

### What next?

1. **Running ROS over a network**
2. **Writing cleaner programs**
3. **Visualizing data with** rviz
4. **Creating message and service types**
5. **Managing coordinate frames with** tf
6. **Simulating with Gazebo**
