# 一，ROS2环境安装

https://docs.ros.org/en/galactic/Installation/Ubuntu-Install-Debians.html

设置语言环境

```
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```



国内镜像源

```bash
sudo sh -c 'echo "deb [arch=$(dpkg --print-architecture)] http://mirror.tuna.tsinghua.edu.cn/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2-latest.list'
```

安装ros的key

```  bash
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```

安装ros

```bash
sudo apt update
sudo apt install ros-galactic-desktop
source /opt/ros/galactic/setup.bash
echo "source /opt/ros/galactic/setup.bash" >> ~/.bashrc
```

测试

```ba
ros2 run demo_nodes_cpp talker
ros2 run demo_nodes_py listener
```

output

```bash
[INFO] [1649046322.467119347] [talker]: Publishing: 'Hello World: 1'
[INFO] [1649046323.467121924] [talker]: Publishing: 'Hello World: 2'
[INFO] [1649046324.467159525] [talker]: Publishing: 'Hello World: 3'
```

如果卸载

```
sudo apt remove ros-galactic-* && sudo apt autoremove
```



# 二，教程

https://docs.ros.org/en/galactic/Tutorials.html

1，里面有win下环境设置命令

```
setx name value
```

这个命令会到环境变量的用户栏目里面,

2，玩turtlesim

```
sudo apt install ros-galactic-turtlesim

ros2 run turtlesim turtlesim_node  启动节点
ros2 run turtlesim draw_square  画方形
```

3，在 ROS 2 中，单个可执行文件（C++ 程序、Python 程序等）可以包含一个或多个节点。

4，给节点临时改名

``` 
ros2 run turtlesim turtlesim_node --ros-args --remap __node:=my_turtle

rqt_graph  图形关系
ros2 node list
ros2 node info
ros2 topic echo /turtle1/cmd_vel    数据可视化
ros2 interface show geometry_msgs/msg/Twist  显示数据类型具体信息
```

发布命令控制海龟

```
ros2 topic pub --once /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}"
```

```
ros2 topic pub --rate 1 /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}"
```





22.04.04 21:35

https://docs.ros.org/en/galactic/Tutorials/Services/Understanding-ROS2-Services.html