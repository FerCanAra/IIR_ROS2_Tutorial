# ROS 2 Tutorial Robotics Students - University of Almería - B. in Informatics Engineering

Repository containing a tutorial to help you understand ROS 2 from scratch in just 4 stages! It is focuses on the morphological and kinematic analysis of mobile robots, as well as the implementation of control and navigation algorithms using the **ROS 2 (Humble/Iron)** middleware and the high-performance **Webots** and **MVSim** simulator.

<img width="355" height="255" alt="image" src="https://github.com/user-attachments/assets/cfbb1315-219f-4558-b141-25f5ac2dc8d5" />
<img width="450" height="350" alt="image7" src="https://github.com/user-attachments/assets/19188ead-06c4-4a75-8e07-18b4cfd6e051" />

*Author: Fernando Cañadas Aránega, PhD student in Agriculture Robotics at the University of Almeria, Spain.*

*Gmail: fernando.ca@ual.es*

*Website: https://linktr.ee/FerCanAra*

<a href="https://arm.ual.es/arm-group/"> 
  <img src="docs/arm-logo2.jpg" width="150" alt="ARM Group Logo" /> 
</a>
<a href="https://www.linkedin.com/company/automatic-robotics-and-mechatronics-research-group/"> 
  <img src="docs/logo2.png" width="55" alt="LinkedIn Logo" /> 
</a>

> **Note:** Process tested with Linux Ubuntu 22.04.05 LTS on 16th April 2026.

------------------------------------------------------------------------

## Prerequisitos

<details>
<summary>Use on native Ubuntu</summary>

- [Linux](https://releases.ubuntu.com/jammy/) (Ubuntu 22.04 recommended).
- [ROS 2 (Humble)](https://docs.ros.org/en/humble/index.html).
- [Environment setup guide](docs/Linux_enviroment_setup.md)

</details>

<details>
<summary>Use on Wndows</summary>

- [Install and configuration vmware pro 17](docs/vmwaresetup.md)

</details>

------------------------------------------------------------------------

## Problem-based learning approach

The programme is divided into four progressive stages:

1.  **Morphological and Kinematic Analysis:** Identification of architectures (Differential vs. Ackermann) and hardware components.
2.  **ROS 2 Environment Setup:** Creation of a structured workspace and dependency management using `rosdep`.
3.  **Perception and Navigation:** Working with simulated sensors, constructing 2D maps, and reactive and deliberative navigation algorithms.
4.  **SLAM with real data:** Working with real sensors to construct three-dimensional environments.

### 1º Stage: Morphological and Kinematic Analysis

Siga estos pasos para replicar el entorno de trabajo:

### 1. Clonar el repositorio y submódulos

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

