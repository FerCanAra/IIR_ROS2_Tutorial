# Environment configuration in Linux

Simply enter the commands in the Linux terminal (Ctrl + Alt + T)

## ROS 2 Humble Install

### Configure locale
```
sudo apt update && sudo apt install locales\
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8\
export LANG=en_US.UTF-8
```
### Install tools
```
sudo apt install software-properties-common\
sudo add-apt-repository universe\
sudo apt update && sudo apt install curl -y
```
### Add ROS 2 repository
```
export ROS_APT_SOURCE_VERSION=\$(curl -s
https://api.github.com/repos/ros-infrastructure/ros-apt-source/releases/latest
\| grep -F 'tag_name' \| awk -F\" '{print \$4}')
```
```
curl -L -o /tmp/ros2-apt-source.deb
https://github.com/ros-infrastructure/ros-apt-source/releases/download/${ROS_APT_SOURCE_VERSION}/ros2-apt-source_${ROS_APT_SOURCE_VERSION}.\$(.
/etc/os-release && echo
${UBUNTU_CODENAME:-${VERSION_CODENAME}})\_all.deb

sudo dpkg -i /tmp/ros2-apt-source.deb
```
### Install ROS 2
```
sudo apt update\
sudo apt upgrade\
sudo apt install ros-humble-desktop
```
### Source ROS 2
```
source /opt/ros/humble/setup.bash
```
------------------------------------------------------------------------

## Additional Packages

### Navigation
```
sudo apt install ros-$ROS_DISTRO-navigation2
sudo apt install ros-$ROS_DISTRO-nav2-bringup
```
### Development tools
```
sudo apt install git\
sudo apt install python3-colcon-common-extensions\
sudo apt install python3-rosdep2
```
### Mapping (MOLA)
```
sudo apt install ros-$ROS_DISTRO-mola
sudo apt install ros-$ROS_DISTRO-mola-state-estimation\
sudo apt install ros-\$ROS_DISTRO-mola-lidar-odometry
```
### Simulation and control
```
sudo apt install gazebo\
sudo apt install ros-${ROS_DISTRO}-turtlebot3-navigation2
sudo apt install ros-$ROS_DISTRO-teleop-twist-keyboard
```
------------------------------------------------------------------------

### src configuration
```
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
git clone git clone https://github.com/cyberbotics/webots_ros2.git
git clone https://github.com/MRPT/mvsim.git --recursive
git clone -b humble-devel https://github.com/ouster-lidar/ouster-ros.git
cd webots_ros2
git submodule update --init --recursive
cd ../..
rosdep update
rosdep install --from-paths src -y --ignore-src
colcon build
echo "source ~/ros2_ws/install/setup.bash" >> ~/.bashrc
```
