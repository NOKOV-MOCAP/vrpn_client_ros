![rolling](https://github.com/NOKOV-MOCAP/vrpn_client_ros/actions/workflows/rolling.yml/badge.svg)
![jazzy](https://github.com/NOKOV-MOCAP/vrpn_client_ros/actions/workflows/jazzy.yml/badge.svg)
![iron](https://github.com/NOKOV-MOCAP/vrpn_client_ros/actions/workflows/iron.yml/badge.svg)
![humble](https://github.com/NOKOV-MOCAP/vrpn_client_ros/actions/workflows/humble.yml/badge.svg)
![foxy](https://github.com/NOKOV-MOCAP/vrpn_client_ros/actions/workflows/foxy.yml/badge.svg)

# vrpn_client_ros

This fork aims to add velocity and acceleration support to ros2

## Usage

```
sudo apt install -y \
     ros-$ROS_DISTRO-geometry-msgs \
     ros-$ROS_DISTRO-tf2 \
     ros-$ROS_DISTRO-tf2-ros \
     ros-$ROS_DISTRO-vrpn 
source /opt/ros/$ROS_DISTRO/setup.bash
cd ~/ros2_ws/src
git clone -b foxy-devel https://github.com/NOKOV-MOCAP/vrpn_client_ros
cd ~/ros2_ws
colcon build --packages-select vrpn_client_ros  --symlink-install
source install/setup.bash
```

nokov@ubuntu:~/ros2_ws/src/vrpn_client_ros/config$ gedit sample.params.yaml

```
vrpn_client_node:
  ros__parameters:
    server: 192.168.2.148
    port: 3883
    frame_id: "world"
    use_server_time: false
    refresh_tracker_frequency: 0.2
    update_frequency: 60.0

```

This is a ROS parameter configuration file for `vrpn_client_node`. Here is a description of each parameter:

- `server` : indicates the IP address of the VRPN server. In this example, the server's IP address is' 192.168.2.148 ', which you can change to 10.1.1.198
- `port` : indicates the port number of the VRPN server. In this example, the port number is' 3883 '.
- `frame_id` : name of the frame on which to publish VRPN data. In this example, the name of the coordinate system is' world '.
- `use_server_time` : a Boolean value that indicates whether the server timestamp is used. If set to true, `vrpn_client_node` will use the timestamp received from the server. If set to false, `vrpn_client_node` will use its own timestamp. In this example, the parameter is set to 'false'.
- `refresh_tracker_frequency` : This is a frequency value indicating how often `vrpn_client_node` refreshes the status of the tracker. In this example, the frequency is refreshed every 5 seconds (0.2 Hz).
- `update_frequency` : This is a frequency value indicating how often `vrpn_client_node` updates data and publishes it to ROS. In this example, this frequency is 60 times per second (60 Hz).

### Launch Default Configuration from Command Line

Run the following command,

```bash
ros2 launch vrpn_client_ros sample.launch.py
```

```Then with `ros2 topic list`, you should be able to see the following topics

```bash
/vrpn_client_node/<tracker_name>/pose
/vrpn_client_node/<tracker_name>/twist # optional when mocap reports velocity data
/vrpn_client_node/<tracker_name>/accel # optional when mocap reports acceleration data
```
where `<tracker_name>` is usually the name of your tracked objects.
