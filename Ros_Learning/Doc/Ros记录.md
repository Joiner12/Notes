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

## 13.fatal error...没有那个文件

<pre><b>/home/ubuntu/ros_imu/src/turn_on_wheeltec_robot/include/wheeltec_robot.h:25:10:</b> <font color="#EF2929"><b>fatal error: </b></font>ackermann_msgs/AckermannDriveStamped.h: 没有那个文件或目录
 #include <font color="#EF2929"><b>&lt;ackermann_msgs/AckermannDriveStamped.h&gt;</b></font>
          <font color="#EF2929"><b>^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~</b></font>
</pre>

### 原因分析

缺少依赖包

### 解决方法

```bash
sudo apt install ros-melodic-ackermann-msgs
```

## 14.查看ros版本

```bash
# 启动ros
roscore
# 新终端
rosparam list.
# 
rosparam get /rosdistro

```

## 15.catkin_make error

### 问题描述

<pre>/usr/bin/ld: 当搜索用于 /home/ubuntu/ros_imu/src/xf_mic_asr_offline/lib/arm64/liboffline_record_lib.so 时跳过不兼容的 -loffline_record_lib
/usr/bin/ld: 找不到 -loffline_record_lib
/usr/bin/ld: 当搜索用于 /home/ubuntu/ros_imu/src/xf_mic_asr_offline/lib/arm64/libhid_lib.so 时跳过不兼容的 -lhid_lib
/usr/bin/ld: 找不到 -lhid_lib
</pre>

### 原因分析

库不兼容

### 解决方案

删除xf_mic_asr_offline功能包再次编译

## 16.查看串口使用情况

```bash
# 查看USB串口
ll /dev/ttyUSB*
dmesg | grep ttyUSB*
# 查看设备外设
ll /dev
```



[Ubuntu串口的操作(查看串口信息、串口助手、串口权限) - 魔比之城 (scielib.com)](https://www.scielib.com/ubuntu-serial-port.html)

## 17.IMU 数据可视化



### reference

1.  
