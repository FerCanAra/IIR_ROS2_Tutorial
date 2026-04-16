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

- **Robotic Morphology:** Study and classification of platforms (Differential, Ackermann, submarine and zoomorphic).
- **Hardware Architecture:** Identification of sensors (LiDAR, IMU, Encoders) and their role in environmental perception.
- **Functional Modelling:** Creation of schematics representing the interaction between physical components and logical control.

### 2º Stage: Morphological and Kinematic Analysis

- **Installing ROS 2:** Ubuntu 22.04 setup procedure and ROS 2.
- **Managing Workspaces:** Structuring the workspace (`ros2_ws`) and cloning integration repositories.
- **Understanding ROS 2**: using nodes, topics and messages via ```ros2 node list```, ```ros2 topic list``` and ```ros2 topic echo ...```

### 3º Stage: Simulación, Sensory Perception and Navigation

- **Webots and MVSim Integration:** Configuring communication between the middleware and the simulator.
- **Monitoring:** Using **Rviz2** to visualise sensor data and transformations (TF) in real time.
- **Data Processing:** Processing information from LiDAR, GPS, IMU, etc.
- **Mapping:** Fundamental concepts of map construction and robot localisation.
- **Control Strategies:** Implementation of **reactive navigation** (obstacle avoidance) and **deliberate navigation** (path planning) algorithms.

### 4º Stage: Real Environment Data

- **Real data playback:** Using ros2bag to play back real Ouster OS0 sensor data.
- **3D SLAM:** Using MOLA to perform 3D mapping of the recorded environment in the rosbag.

