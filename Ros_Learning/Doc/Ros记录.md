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
3. [VNCViewer实现与WIN端文本复制粘贴_Erpim的博客-CSDN博客](https://blog.csdn.net/qq_35414569/article/details/80259503?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.baidujs&dist_request_id=1328642.22533.16156117962279547&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.baidujs)
3. [Vim的保存和退出命令 - 简书 (jianshu.com)](https://www.jianshu.com/p/b6d7153c83f1)
3. [Ubuntu:由于没有公钥，无法验证下列签名_天线狗子的博客-CSDN博客_ubuntu由于没有公钥,无法验证下列签名](https://blog.csdn.net/qq_37236149/article/details/111240085)
3. [如何将Ubuntu升级到18.04最新版 - 云+社区 - 腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1174343)
3. [Ubuntu安装ROS2并编写自己的程序 - 古月居 (guyuehome.com)](https://www.guyuehome.com/33808)
3. [Building ROS 2 on Linux — ROS 2 Documentation: Eloquent documentation](https://docs.ros.org/en/eloquent/Installation/Linux-Development-Setup.html)
3. [ROS探索总结（二十一）——如何发布里程计消息 - 古月居 (guyuehome.com)](https://www.guyuehome.com/332)
3. [SLAM+语音机器人DIY系列：（六）SLAM建图与自主避障导航——4.多目标点导航及任务调度 - 小虎哥哥爱学习 - 博客园 (cnblogs.com)](https://www.cnblogs.com/hiram-zhang/p/10416104.html)
3. [从零搭建一辆ROS小车（二）发布里程计数据在rviz中显示 - 码上快乐 (codeprj.com)](https://www.codeprj.com/blog/bed43d1.html)
3. [linux命令之sh的用法_xiaozhuangyumaotao的博客-CSDN博客_linux sh命令](https://blog.csdn.net/xiaozhuangyumaotao/article/details/105645925)
3. [GPG配置、命令、实例与apt-key密钥测试 - usmile - 博客园 (cnblogs.com)](https://www.cnblogs.com/usmile/p/12873604.html)

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

## 9.安装ROS2()



```shell
# 1.设置本地环境
locale  # check for UTF-8

sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

locale  # verify settings
# 2.软件源
sudo apt update && sudo apt install curl gnupg2 lsb-release
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
# 3.添加代码仓库到源
sudo sh -c 'echo "deb [arch=amd64,arm64] http://packages.ros.org/ros2/ubuntu `lsb_release -cs` main" > /etc/apt/sources.list.d/ros2-latest.list'
# 4.更新软件
sudo apt update
# 5.安装ROS2桌面版 
sudo apt install ros-eloquent-desktop
# 6.自动补全工具
sudo apt install -y python3-pip
pip3 install -U argcomplete
# 7.安装编译工具
sudo apt install python3-colcon-common-extensions
# 8.安装依赖和ROS工具
# 无法定位bulid-essential
sudo apt update && sudo apt install -y bulid-essential cmake git python3-colcon-common-extensions python3-pip python-rosdep python3-vcstool-wget
# 使用pip3安装测试功能包，执行以下指令：
python3 -m pip install -U argcomplete flake8 flake8-blind-except flake8-builtins flake8-class-newline flake8-comprehensions flake8-deprecated flake8-docstrings flake8-import-order flake8-quotes pytest-repreat pytest-rerunfailures pytest pytest-cov pytest-runner stuptools
# 安装FAST-RTPS依赖项
sudo apt install --no-install-recommends -y libasio-dev libtinyxml2-dev
# 安装Cyclone DDS依赖项
sudo apt install --no-install-recommends -y libcunit1-dev
# 9.环境配置
sudo gedit ~/.bashrc
# 添加
alias initros1="source /opt/ros/melodic/setup.bash"
alias initros2="source /opt/ros/eloquent/setup.bash"
# 保存生效
source ~/.bashrc
# 10.测试
initros2
ros2 run demo_nodes_cpp talker
ros2 run demo_nodes_py listener
```

## 10.ROS主机搭建NFS服务

```shell
在Ros主机上搭建NFS服务器
一、服务端执行：
1、安装必备包
在机器人中安装nfs服务端
sudo apt-get install nfs-kernel-server
2、创建要共享的目录文件夹
sudo -p mkdir /mnt

3、编辑配置文件
①添加NFS共享目录
sudo nano /etc/exports 
/home/wheeltec/wheeltec_rebot  *(rw,sync,no_root_squash)
②给挂载的目录设置权限以及修改文件用户
sudo chmod  -R  777  /home/wheeltec/wheeltec_robot
sudo chown  -R  777  nobody  /home/wheeltec/wheeltec_robot

4、启动服务
sudo /etc/init.d/nfs-kernel-server start  
sudo  /etc/init.d/nfs-kernel-server restart 	
先启动NFS再重启NFS

二、客户端
1、安装nfs-utils和portma包
sudo apt-get install nfs-common portmap
2、创建一个提供挂载的目录
sudo mkdir /mnt/mount_nfs
3、挂载
 sudo  mount  -t  nfs  -o  nolock  192.168.0.100:/home/wheeltec/wheeltec_robot  /mnt
```

## 11.烧录

1. [Operating system images – Raspberry Pi](https://www.raspberrypi.com/software/operating-systems/)
2. [Index of /ubuntu-cdimage/ubuntu/releases/18.04.5/release/ | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/ubuntu-cdimage/ubuntu/releases/18.04.5/release/)
3. [树莓派4b之镜像烧录（手把手完整版）_六五酥的博客-CSDN博客_树莓派4b 镜像](https://blog.csdn.net/qq_27149279/article/details/105308588)
4. [树莓派4B安装ubuntu18.04.4和ROS并测试激光雷达_蜗小侠的博客-CSDN博客](https://blog.csdn.net/qq_35898865/article/details/105065259)

## 12.ROS基础

### 1.创建工作空间

<1> 将要创建的工作空间文件夹是在~/catkin_ws/src/中。 若新创建则使用下面命令。  

````bash
# 创建工作空间
mkdir -p ros_ws_1/src
cd ros_ws_1/src/
# 工作空间初始化
catkin_init_workspace

````

<2> 创建完工作空间文件夹后， 里面并没有问的文件夹， 只有CMkkeList.txt。 下一步是编译工作空间， 使用下面的命令：  

```bash
cd ~/ros_ws_1
catkin_make
```

编译完成后， 查看catkin_ws文件目录， 可以看到上面的编译命令创建了build和devel文件夹。

<3> 使用命令， 完成配置 

```bash
~/ros_ws_1$ source devel/setup.bash
```

<4> 添加程序包到全局路径并使之生效（如果已经添加过则忽略此步骤）

```bash
$ echo "source ~/ros_ws_1/devel/setup.bash" >> ~/.bashrc
$ source ~/.bashrc
```

要想保证工作空间已配置正确需确保ROS_PACKAGE_PATH环境变量包含你的工作空间目录， 采用以下命令查看：  

```bash
$ echo $ROS_PACKAGE_PATH
/home/<youruser>/catkin_ws/src:/opt/ros/kinetic/share
```

### 2.工作空间目录解析 

使用linux下的tree树状目录结构打开我们创建的catkin_ws工作空间（ 如下图所示） ，可以看到该工作空间下包含build、 devel和src三个文件夹， 有时候编译也会出现更多的信息，但是这三个文件夹是catkin编译系统默认的， 每个文件夹都是一个具有不同功能的空间。  

```BASH
tree -L 2 ros_ws_1
```

:large_blue_diamond: **源文件空间（The Source space）** : 在源空间（src 文件夹） 放置了功能包、 项目、克隆包等， 这个空间最重要的是 CMakeLists.txt。 当你在工作空间中配置功能包时， src 文件夹 CMakeList.txt 调用 make。 这个文件是通过 catkininitworkspace 命令创建的。  

:large_orange_diamond: **编译空间（The Build space）** ： 在build文件夹里， CMake和catkin为功能包和项目保存缓存信息、 配置、 和其他中间文件。  

:large_orange_diamond: **开发空间（The Development space） ：** devel 文件夹用来保存编译后的程序， 编译生成的目标文件包括头文件， 动态链接库， 静态链接库， 可执行文件等环境变量， 这些无需安装就能用来测试的程序。 一旦通过测试， 就可以安装或者导出功能包与其他开发人员分享。  

### 3.catkin编译包 

catkin编译包有两个选项， 一个是使用标准的CMake工作流程， 通过此方法编译一个包：  

```bash
$ cmake packageToBuild/
$ make
```

使用catkin_make命令行编译所有的包：  

```bash
$ cd workspace(工作空间目录)
$ catkin_make
```

### 4.功能包的开发编译 

```bash
smileface@smileface-VirtualBox:~/Desktop/ros_ws_1/src$ catkin_create_pkg test_tutorial roscpp rospy std_msgs
Created file test_tutorial/CMakeLists.txt
Created file test_tutorial/package.xml
Created folder test_tutorial/include/test_tutorial
Created folder test_tutorial/src
Successfully created files in /home/smileface/Desktop/ros_ws_1/src/test_tutorial. Please adjust the values in package.xml.

```

创建功能包指令：

```bash
catkin_create_pkg <package_name> [depend1] [depend2] [depend3]
```

```cpp
#include "ros/ros.h"
#include "std_msgs/String.h"
#include <sstream>
int main(int argc， char **argv)
{
    ros::init(argc， argv， "talker");
    ros::NodeHandle n;
    ros::Publisher chatter_pub = n.advertise<std_msgs::String>("chatter"， 1000);
    ros::Rate loop_rate(10);
    int count = 0;
    while (ros::ok())
    { 
        std_msgs::String msg;
        std::stringstream ss;
        ss << "hello" <<count;
        msg.data = ss.str();
        ROS_INFO("%s"， msg.data.c_str());
        chatter_pub.publish(msg);
        ros::spinOnce();
        loop_rate.sleep();
        ++count;
    }
    return 0;
}
```

### 5.ROS节点

一个节点其实只不过是ROS程序包中的一个可执行文件。 ROS节点可以使用ROS客户库与其他节点通信。 节点可以发布或接收一个话题。 节点也可以提供或使用某种服务。  

```shell
# 运行所有ROS程序必须启动
roscore
```

**节点处理工具**

```shell
$ rosnode
rosnode is a command-line tool for printing information about ROS Nodes.

Commands:
	rosnode ping	test connectivity to node
	rosnode list	list active nodes
	rosnode info	print information about node
	rosnode machine	list nodes running on a particular machine or list machines
	rosnode kill	kill a running node
	rosnode cleanup	purge registration information of unreachable nodes

Type rosnode <command> -h for more detailed usage, e.g. 'rosnode ping -h'

```

### 6.ROS话题

话题是节点用来传输数据的总线。 通过话题进行消息路由不需要节点之间直接连接， 这就意味着发布者和订阅者之间不需要知道彼此的存在。 同一个话题可以有多个订阅者， 也可以有多个发布者。 话题默认采用TCP/IP长连接的方式传输。话题之间的通信是通过在节点之间发送ROS消息实现的。 对于发布器(turtleteleopkey)和订阅器(turtulesim_node)之间的通信， 发布器和订阅器之间必须发送和接收相同类型的消息。 这意味着话题的类型是由发布在它上面的消息类型决定的。 使用rostopic type命令可以查看发布在某个话题上的消息类型。  

```shell
# 列出节点话题清单
$ rostopic list
rostopic is a command-line tool for printing information about ROS Topics.

Commands:
	rostopic bw	display bandwidth used by topic
	rostopic delay	display delay of topic from timestamp in header
	rostopic echo	print messages to screen
	rostopic find	find topics by type
	rostopic hz	display publishing rate of topic    
	rostopic info	print information about active topic
	rostopic list	list active topics
	rostopic pub	publish data to topic
	rostopic type	print topic or field type

Type rostopic <command> -h for more detailed usage, e.g. 'rostopic echo -h'

```



### 7.rqt_graph

rqt_graph是rqt程序包中的一部分， 它可以创建一个显示当前系统运行情况的动态图形 。

打开新的终端

```bash
$ rosrun rqt_graph rqt_graph
```

rqt_plot命令可以实时显示一个发布到某个话题上的数据变化图形。   

```bash
$ rosrun rqt_plot rqt_plot
```

