# RPLidar Setup Guide for Jetson Orin nano and ROS 2 Humble

## Prerequisites
- Ubuntu 22.04 on Jetson
- ROS 2 Humble installed
- RPLidar A1 hardware

## Installation

1. Install dependencies:
```bash
sudo apt update
sudo apt install -y ros-humble-ament-cmake-auto
```

2. Create workspace and clone repository:
```bash
mkdir -p ~/rplidar_ws/src
cd ~/rplidar_ws/src
git clone https://github.com/babakhani/rplidar_ros2.git
```

3. Build the package:
```bash
cd ~/rplidar_ws
source /opt/ros/humble/setup.bash
colcon build --symlink-install
```

4. Add environment setup to bashrc:
```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
echo "source ~/rplidar_ws/install/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

## Usage

1. Verify package installation:
```bash
ros2 pkg list | grep rplidar
```

2. Launch RPLidar:
```bash
ros2 launch rplidar_ros view_rplidar.launch.py
```

3. View raw data:
```bash
ros2 topic echo /scan
```

## Visualization with Rviz2

For visualization on a remote machine:
1. Install ROS 2 Humble on your desktop/laptop
2. Configure ROS_DOMAIN_ID to match Jetson
3. Run Rviz2:
```bash
rviz2
```

In Rviz2, change "Fixed Frame" from "map" to "laser" or "base_link" in the "Global Options" panel

4. Add LaserScan display and set topic to /scan
