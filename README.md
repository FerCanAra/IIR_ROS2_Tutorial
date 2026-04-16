# ROS 2 Tutorial Robotics Students - University of Almería - B. in Informatics Engineering

Repository containing a tutorial to help you understand ROS 2 from scratch in just 6 hours! It is focuses on the morphological and kinematic analysis of mobile robots, as well as the implementation of control and navigation algorithms using the **ROS 2 (Humble/Iron)** middleware and the high-performance **Webots** and **MVSim** simulator.

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

El desarrollo se divide en fases progresivas (enfoque ABP híbrido):

1.  **Análisis Morfológico y Cinemático:** Identificación de arquitecturas (Diferencial vs. Ackermann) y componentes hardware.
2.  **Configuración del Entorno ROS 2:** Creación de un *workspace* estructurado y gestión de dependencias con `rosdep`.
3.  **Simulación y Control:** Integración de Webots con ROS 2 para el control de movimiento mediante nodos de teleoperación.
4.  **Percepción y Navegación:** Trabajo con sensores reales/simulados, construcción de mapas y algoritmos de navegación reactiva y deliberada.

## 🔧 Instalación y Configuración

Siga estos pasos para replicar el entorno de trabajo:

### 1. Clonar el repositorio y submódulos

mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
git clone <url-de-tu-repositorio>
cd webots_ros2
git submodule update --init --recursive















------------------------------------------------------------------------

## 🖥️ 1. Virtual Machine Setup

1.  Registrarse en [Broadcom](https://support.broadcom.com/).
2.  Descargar [VMware Workstation Pro](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion).
3.  Ver este [documento](https://drive.google.com/file/d/1kVDq_wucM1GCC-6ea2r2fvFyyT6knKXH/view?usp=drive_link) para ver el paso a paso.

------------------------------------------------------------------------

## 🐧 2. Ubuntu Installation

Download [Ubuntu 22.04.5 LTS](https://releases.ubuntu.com/jammy/).

Recommended configuration:

-   Disk: 30 GB\
-   RAM: 8 GB\
-   CPU: 4 cores

Steps:

1.  Create a new virtual machine\
2.  Select the Ubuntu ISO\
3.  Follow the installation wizard

------------------------------------------------------------------------

<a name="Congiguration_Seup"></a>

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

## 📦 4. Additional Packages

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

## 🧪 5. Workspace Setup
```
mkdir -p \~/journal/ieee_iot_2\
cd \~/journal/ieee_iot_2
```
Descomprime el [archivo comprimido](https://drive.google.com/file/d/1MCiqBNdE58fHB75JSwNnDfkTiPTIqoyD/view?usp=drive_link) de Drive y descomprímelo en ```/journal/ieee_iot_2```. Entonces:
```
rosdep update\
rosdep install --from-paths src -y --ignore-src
colcon build --symlink-install --cmake-args -DCMAKE_BUILD_TYPE=Releaseros -DYOLOX_USE_OPENVINO=ON
. install/setup.bash
echo "source \~/ros2_ws/install/setup.bash" \>\> \~/.bashrc
```
------------------------------------------------------------------------

## 🚀 6.Lanzar simulación completa
```
ROS2_MQTT_bridge.sh
```
------------------------------------------------------------------------

## 📚 License

BSD 3-Clause License

------------------------------------------------------------------------

## 👨‍🏫 Authors

Fernando Cañadas Aránega

Todo en [Drive](https://drive.google.com/drive/folders/1HC5idcXOKwYxiy8K2DE4wB4wFAAT1ZA7?usp=sharing).

University of Almería\
Department of Computer Science\
Area of Systems Engineering and Automation
