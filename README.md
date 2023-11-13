# vrpn_client_ros
This fork aims at porting the original code from the kinetic-devel branch to ROS2.

## Requirements

The code requires VRPN to work. Unfortunately, currently the package is only
available in melodic and older ROS releases and can be installed with:
```
    apt-get install ros-melodic-vrpn
```

If you want to stick to ROS2 or do not have access to melodic packages you can
clone the following repository to the src folder of your ros_overlay_ws:
```
git clone --single-branch --branch debian/melodic/vrpn git@github.com:ros-drivers-gbp/vrpn-release.git

```
## Usage
```
sudo apt install ros-foxy-vrpn
source /opt/ros/foxy/setup.bash
cd ~/ros2_ws/src
git clone -b foxy-devel https://github.com/NOKOV-MOCAP/vrpn_client_ros
cd ~/ros2_ws
colcon build --packages-select vrpn_client_ros  --symlink-install
source install/setup.bash
```
nokov@ubuntu:~/ros2_ws/src/vrpn_client_ros/config$ gedit sample.params.yaml

这是一个`vrpn_client_node`的ROS参数配置文件。以下是每个参数的说明：

- `server`: VRPN服务器的IP地址。在这个例子中，服务器的IP地址是`192.168.0.107`, 这里你可以修改为10.1.1.198

- `port`: VRPN服务器的端口号。在这个例子中，端口号是`3883`。

- `frame_id`: 用于发布VRPN数据的坐标系的名称。在这个例子中，坐标系的名称是`world`。

- `use_server_time`: 一个布尔值，表示是否使用服务器的时间戳。如果设置为`true`，`vrpn_client_node`将使用从服务器接收到的时间戳。如果设置为`false`，`vrpn_client_node`将使用它自己的时间戳。在这个例子中，这个参数被设置为`false`。

- `refresh_tracker_frequency`: 这是一个频率值，表示`vrpn_client_node`多久刷新一次跟踪器的状态。在这个例子中，这个频率是每5秒（0.2 Hz）刷新一次。

- `update_frequency`: 这是一个频率值，表示`vrpn_client_node`多久更新一次数据并发布到ROS。在这个例子中，这个频率是每秒30次（30 Hz）。

请注意，这些参数的具体含义和使用可能会根据你的具体使用场景和`vrpn_client_node`的实现有所不同。


