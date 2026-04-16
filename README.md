# ROS 2 Tutorial Robotics Students - University of Almería - B. in Informatics Engineering

Repository containing a tutorial to help you understand ROS 2 from scratch in just 4 stages! It is focuses on the morphological and kinematic analysis of mobile robots, as well as the implementation of control and navigation algorithms using the **ROS 2 (Humble/Iron)** middleware and the high-performance **Webots** and **MVSim** simulator.

<img width="355" height="255" alt="image" src="https://github.com/user-attachments/assets/cfbb1315-219f-4558-b141-25f5ac2dc8d5" />
<img width="450" height="350" alt="image7" src="https://github.com/user-attachments/assets/19188ead-06c4-4a75-8e07-18b4cfd6e051" />

*Author: Fernando Cañadas Aránega, PhD student in Agriculture Robotics at the University of Almeria, Spain.*

*[Automatic, Robotics and Mechatronics](https://arm.ual.es/arm-group/) group, Departments of Informatics*

*Gmail: fernando.ca@ual.es*

*Website: https://linktr.ee/FerCanAra*

<a href="https://arm.ual.es/arm-group/"> 
  <img src="docs/arm-logo2.jpg" width="150" alt="ARM Group Logo" /> 
</a>
<a href="https://www.linkedin.com/company/automatic-robotics-and-mechatronics-research-group/"> 
  <img src="docs/logo2.png" width="55" alt="LinkedIn Logo" /> 
</a>

> **Note:** Process tested with Linux Ubuntu 22.04 LTS on 16th April 2026.

------------------------------------------------------------------------

## Installing and setup your environment

<details>
<summary>Use on native Ubuntu</summary>

- [Linux](https://releases.ubuntu.com/jammy/) (Ubuntu 22.04 recommended).
- [ROS 2 (Humble)](https://docs.ros.org/en/humble/index.html).
- [Environment setup guide](docs/Linux_enviroment_setup.md)

</details>

<details>
<summary>Use on Wndows with virtual machine</summary>

- [Install and configuration vmware pro 17](docs/vmwaresetup.md)

</details>

------------------------------------------------------------------------

## Problem-based learning approach

The programme is divided into four progressive stages:

<details>
<summary>1º Stage: Morphological and Kinematic Analysis</summary>
  
- Robotic Morphology: Study and classification of platforms (Differential, Ackermann, submarine and zoomorphic).
- Hardware Architecture: Identification of sensors (LiDAR, IMU, Encoders) and their role in environmental perception.
- Functional Modelling: Creation of schematics representing the interaction between physical components and logical control.
  
</details>

<details>
<summary>2º Stage: Morphological and Kinematic Analysis</summary>

- Installing ROS 2: Ubuntu 22.04 setup procedure and ROS 2.
- Managing Workspaces: Structuring the workspace (`ros2_ws`) and cloning integration repositories. 
- Understanding ROS 2: using nodes, topics and messages via ```ros2 node list```, ```ros2 topic list``` and ```ros2 topic echo ...```
  
</details>

<details>
<summary>3º Stage: Simulación, Sensory Perception and Navigation</summary>

- Webots and MVSim Integration: Configuring communication between the middleware and the simulator.
- Monitoring: Using Rviz2 to visualise sensor data and transformations (TF) in real time.  
- Data Processing: Processing information from LiDAR, GPS, IMU, etc.  
- Mapping: Fundamental concepts of map construction and robot localisation.  
- Control Strategies: Implementation of **reactive navigation** (obstacle avoidance) and **deliberate navigation** (path planning) algorithms.

</details>

<details>
<summary>4º Stage: Real Environment Data</summary>

- Real data playback: Using ros2bag to play back real Ouster OS0 sensor data.
- 3D SLAM: Using MOLA to perform 3D mapping of the recorded environment in the rosbag.
  
</details>

------------------------------------------------------------------------

## Tutorial for ROS 2 PBL

<details>
<summary>Exercise 1. Initialising ROS 2</summary>

Open a terminal (`Ctrl+Alt+T`) and execute the following command to initialise the ROS 2 environment variables:
```
source /opt/ros/humble/setup.bash
```
This command must be executed in every new terminal session. To verify the installation, run:
```
echo $ROS_DISTRO
```
In ROS 2, a Node is a discrete process responsible for a specific task (e.g., sensor data acquisition or actuator control). To visualize this, run a publisher node:
```
ros2 run demo_nodes_cpp talker
```
In a second terminal, launch a subscriber node:
```
ros2 run demo_nodes_py listener
```
The "talker" node publishes messages while the "listener" node subscribes to them. You can audit active nodes using:
```
ros2 node list
```
A Topic acts as a communication bus for nodes to exchange messages asynchronously via a publisher/subscriber model. To list active topics, execute:
```
ros2 topic list
```
To inspect the message type associated with a specific topic (e.g., /chatter):
```
ros2 topic type /chatter
```
ROS 2 provides tools to monitor and interact with the data stream in real-time:
- Monitor messages: View live data circulating through a topic:
```
ros2 topic echo /chatter
```
- Manual injection: Publish a custom message directly from the CLI:
```
ros2 topic pub /chatter std_msgs/msg/String "data: 'Hello ROS'"
```
- Performance analysis: Measure the publishing frequency (Hz) to estimate system latency:
```
ros2 topic hz /chatter
```
</details>

<details>
<summary>Exercise 2. Interaction with simulators and visualisers in ROS</summary>

Once the core ROS 2 concepts are understood, the next stage involves interacting with complex packages within the ROS ecosystem. This section focuses on deploying a mobile robot simulator to analyze sensor data and visualization tools.

Execute the following launch file to start the environment:
```
ros2 launch mvsim demo_jackal.launch.py
```
Upon execution, MVsim emerge (MVSim is a lightweight, realistic 2D engine for mobile robotics. In the default scene, you will observe):

<img width="350" height="150" alt="image" src="https://github.com/user-attachments/assets/9d357bbf-08ef-4c8f-b32a-f84e6f692d57" />

where:

- Yellow Robot: A Jackal unmanned ground vehicle (UGV).
- Blue Cubes: Obstacles (some in motion) for collision avoidance testing.
- Black Lines: Real-time 2D LiDAR scan rays measuring distances.
- Blue Points: 3D point cloud data generated by an RGB-D camera.

Also, RViz is a 3D visualizer that displays data exchanged within the ROS system. Unlike the simulator, RViz does not calculate physics; it only renders what the robot "perceives".

<img width="350" height="160" alt="image" src="https://github.com/user-attachments/assets/b6c3c173-ed48-4c92-b75b-cc61f8973b8c" />

Key elements in the Displays panel:
- RGB: Visual feed from the robot’s camera.
- LaserScan: Graphical representation of LiDAR measurements.
- RGBD Cloud: Detailed 3D point cloud from the depth sensor.
- TF (Transform Tree): Displays the spatial relationship and hierarchy between the robot's reference frames and its sensors.

To validate the system's dynamic response:

- Focus your mouse on the MVSim window.
- Press the W key to move the robot forward.
- Observe how the sensor data (LiDAR and Point Clouds) updates in real-time within RViz as the robot interacts with the environment.

</details>

<details>
<summary>Exercise 3. Concepts relating to sensor readings</summary>

In this stage, the focus shifts to a high-fidelity 3D environment using **Webots**. This simulator allows for designing, programming, and testing robots in virtual scenarios that integrate realistic physics, collisions, and complex environmental interactions before deploying to real-world systems.

To initialize the TurtleBot3 simulation within the ROS 2 ecosystem, execute the following launch file:
```
ros2 launch webots_ros2_turtlebot robot_launch.py
```
Upon execution, the Webots interface will load the scenario featuring the robot and its associated communication infrastructure (Topics).

<img width="300" height="150" alt="image" src="https://github.com/user-attachments/assets/c40d53be-0203-4e79-88c3-03c84d03a010" />
<img width="300" height="180" alt="image" src="https://github.com/user-attachments/assets/ba37289d-debd-499a-9e36-36015ebc42c3" />

The simulated robot is equipped with a comprehensive sensor array that publishes data to specific ROS topics. Key sensors include:

- GPS: Provides global positioning data within the simulated environment via the /TurtleBot3Burger/gps topic.
- Encoders: Integrated into the wheels to measure displacement and rotational velocity, allowing the calculation of odometry published in /odom.
- IMU (Inertial Measurement Unit): Tracks linear acceleration, angular velocity, and orientation, publishing to the /imu topic.
- 2D LIDAR: A laser scanner for obstacle detection, generating distance measurements published as a point cloud in /scan/point_cloud.

To interact with the robot and observe real-time sensor updates, a manual control node can be used. Open a new terminal and run:
```
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

<img width="350" height="200" alt="image" src="https://github.com/user-attachments/assets/4f2ee020-d74d-49c9-aaea-6d6a8f68795c" />

Control Instructions:
- Use the keyboard keys displayed in the terminal to send velocity commands (teleoperation).
- As the robot moves, you can monitor how the GPS, Odometry, and LIDAR topics dynamically update their values based on the robot's interaction with the 3D world.

</details>

<details>
<summary>Exercise 4. SLAM</summary>

In this advanced module, the **SLAM (Simultaneous Localization and Mapping)** algorithm is implemented using the **Webots** simulator and the `slam_toolbox`. The core objective is to enable the mobile robot to construct a consistent map of an unknown environment while simultaneously estimating its own pose (position and orientation) within that map.

To initialize the mapping system, you must execute the following components in separate terminals:
```
ros2 launch webots_ros2_turtlebot robot_launch.py
```
Using the asynchronous online mode of slam_toolbox:
```
ros2 launch slam_toolbox online_async_launch.py
```
Run Rviz2:
```
rviz2
```
By default, RViz2 will open without active displays. 

<img width="250" height="200" alt="image" src="https://github.com/user-attachments/assets/72f26052-c5f5-494a-a0a0-40f3ad0e92d0" />

To visualize the mapping process, manually add the following elements via the "Add" button (bottom left):

<img width="150" height="120" alt="image" src="https://github.com/user-attachments/assets/9c161b86-42fc-4c90-932a-d77753f3a030" />

- By Display Type: Add RobotModel (to see the robot's structure).
- By Display Type: Add TF (to visualize the transform tree and reference frames).
- By Topic: Add Map (to visualize the occupancy grid being generated).

To create a complete map, you must navigate the robot throughout the environment using the teleoperation node:
```
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```
Once the environment is fully explored and the map is consistent:

<img width="320" height="200" alt="image" src="https://github.com/user-attachments/assets/80a82c55-17af-4786-ad1d-9e896ec73a33" />

Save the results by executing:
```
ros2 run nav2_map_server map_saver_cli -f my_map
```
Output Files:
- my_map.pgm: An occupancy grid image where: White is Free space, black is Obstacles, and gray is Unexplored/Unknown areas.
- my_map.yaml: Metadata file containing parameters such as resolution, origin, and thresholds.

</details>

<details>
<summary>Exercise 5. Concepts relating to location and navigation</summary>
  
This section covers the implementation of **AMCL (Adaptive Monte Carlo Localization)** and autonomous navigation using the **Nav2** stack. The goal is to allow the robot to estimate its pose within a pre-existing map and navigate to a specific goal avoiding obstacles. AMCL is a probabilistic localization system that uses a **Particle Filter** to track the pose of a robot against a known map.

To start the simulation with the navigation stack and the pre-loaded map enabled, use the `nav` argument:
```
ros2 launch webots_ros2_turtlebot robot_launch.py nav:=true
```
The navigation system uses two main costmaps to plan and execute trajectories:

<img width="325" height="170" alt="image" src="https://github.com/user-attachments/assets/80b8fc72-50e6-4887-bbce-27b6f39e1681" />


- Global Costmap (Deliberative): Used by the global planner (based on Dijkstra/A* algorithms) to calculate the optimal path from the current position to the goal.
- Local Costmap (Reactive): A smaller, dynamic window around the robot used for obstacle avoidance in real-time, adjusting the trajectory to account for unforeseen obstacles.

You can interact with the navigation system directly through the RViz2 interface:

- Locate the "Nav2 Goal" tool in the top toolbar of RViz.
- Click on a point in the map and drag the green arrow to set the desired orientation.
- The system will automatically calculate the path and the robot will begin moving towards the target, dynamically avoiding obstacles.

<img width="360" height="210" alt="image" src="https://github.com/user-attachments/assets/e4400cc9-87e5-4b07-b3ee-df984d2b9d2c" />

</details>

<details>
<summary>Exercise 6. Practical concepts in sensor reading and navigation</summary>

This module focuses on processing real sensor data captured at the University of Almería (UAL). The dataset includes high-density 3D LiDAR point clouds and IMU telemetry recorded during a field test in María (Almería).

The data is stored in a `rosbag2` format, which allows for the playback of recorded sensor streams as if they were happening in real-time. Ensure the following folder is in your `ros2_ws`:
- **Directory:** `rosbag2_2023_11_29-11_00_24_0/`
- **Files:** `metadata.yaml` and the database `.db3`.

To visualize the 3D data, the Ouster LiDAR ROS 2 driver must be installed and compiled. Then, run:
```
ros2 launch ouster_ros replay.launch.xml bag_file:=rosbag2_2023_11_29-11_00_24_0/
```
Upon launching, RViz2 will display the 3D point cloud from the Ouster OS0 LiDAR, which generates approximately 5.2 million points per second, providing a high-resolution representation of the environment.

<img width="450" height="150" alt="image" src="https://github.com/user-attachments/assets/978eec26-cd9e-4c36-a1ff-fde2bcbfc01b" />


Upon launching, RViz2 will display the 3D point cloud from the Ouster OS0 LiDAR, which generates approximately 5.2 million points per second, providing a high-resolution representation of the environment.
```
sudo apt install \
ros-humble-mola \
ros-humble-mola-state-estimation \
ros-humble-mola-lidar-odometry
```
Run the following command to start the mapping process using IMU-based motion compensation:
```
ros2 launch mola_lidar_odometry ros2-lidar-odometry.launch.py \
 mola_deskew_method:=MotionCompensationMethod::IMU \
 lidar_topic_name:=/ouster/points \
 imu_topic_name:=/ouster/imu \
 mola_tf_base_link:=os_sensor
 ```
The system will open the Molaviz graphical interface, progressively generating a detailed 3D map. This demonstrates how modern algorithms integrate:

- 3D LiDAR Data: For spatial structure.
- IMU Integration: For motion compensation and orientation tracking.
- LiDAR Odometry: To estimate the sensor's trajectory and reconstruct the environment without external positioning (like GPS).

<img width="450" height="350" alt="image7" src="https://github.com/user-attachments/assets/19188ead-06c4-4a75-8e07-18b4cfd6e051" />

</details>
