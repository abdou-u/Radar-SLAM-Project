# Offline Pipeline

The offline pipeline allows for post-processing and detailed analysis of radar data using ROS and other tools. This pipeline is based on the Radarize framework, which requires multiple dependencies and setup steps.

## Prerequisites

Ensure you have Ubuntu and ROS Noetic installed. The following instructions guide you through setting up the environment and dependencies.

### Step 1: Update and Install Essential Packages

- `sudo apt update`
- `sudo apt install vim git curl ninja-build stow lsb-release python3-pip imagemagick`

### Step 2: Install ROS Noetic

1. Add the ROS repository:
   - `sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'`
   - `curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -`
   - `sudo apt update`

2. Install ROS Noetic:
   - `sudo apt install ros-noetic-desktop-full`

3. Add the ROS setup script to your `.bashrc`:
   - `echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc`
   - `source ~/.bashrc`

4. Install additional ROS dependencies:
   - `sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential`
   - `sudo rosdep init`
   - `rosdep update`

### Step 3: Install xwr_raw_ros

1. Install additional ROS tools:
   - `sudo apt install ros-noetic-catkin python3-catkin-tools`

2. Clone the xwr_raw_ros repository:
   - `mkdir -p ~/catkin_ws/src`
   - `cd ~/catkin_ws/src`
   - `git clone https://github.com/ConnectedSystemsLab/xwr_raw_ros.git`

3. Install dependencies and build:
   - `cd ~/catkin_ws`
   - `rosdep install --from-paths src --ignore-src -iry`
   - `pip install -r src/xwr_raw_ros/requirements.txt`
   - `catkin build`

4. Add the workspace setup script to your `.bashrc`:
   - `echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc`
   - `source ~/.bashrc`

### Step 4: Install Cartographer

1. Initialize and update the Cartographer workspace:
   - `wstool init src`
   - `wstool merge -t src https://raw.githubusercontent.com/cartographer-project/cartographer_ros/master/cartographer_ros.rosinstall`
   - `wstool update -t src`

2. Remove `libabsl-dev` from `package.xml`:
   - `vim src/cartographer/package.xml`

3. Install dependencies and build Cartographer:
   - `rosdep install --from-paths src --ignore-src --rosdistro=${ROS_DISTRO} -y`
   - `src/cartographer/scripts/install_abseil.sh`
   - `sudo ln -s /usr/bin/empy3 /usr/bin/empy`
   - `catkin_make_isolated --install --use-ninja`

### Step 5: Install Miniconda

1. Download and install Miniconda:
   - `sudo mkdir /opt/conda`
   - `sudo chmod 777 /opt/conda`
   - `cd /opt/conda`
   - `curl -o miniconda.sh https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh`
   - `bash miniconda.sh -b -u -p /opt/conda`
   - `rm /opt/conda/miniconda.sh`

2. Initialize Conda:
   - `conda init`
   - `conda config --set auto_activate_base false`

### Step 6: Install Radarize

1. Clone the Radarize repository and set up the environment:
   - `conda env create -f env.yaml`
   - `conda activate radarize_ae`
   - `pip install -e .`

2. Move Cartographer files:
   - Move files from the `cartographer/` folder (in the repository) to `<catkin_ws>/install_isolated/share/cartographer_ros/`.

## Launching the Offline Pipeline

### Launch xwr_raw_ros Node

1. Configure the network and permissions:
   - `sudo ip a add 192.168.33.30/24 dev enxa0cec89de3b4`
   - `chmod 666 /dev/ttyACM*`
   - `chown root:koitu /dev/ttyACM*`

2. Launch the radar visualization node:
   - `roslaunch xwr_raw_ros radar_visra_c.launch`

This completes the setup and launch instructions for the offline pipeline. You can use this setup for offline data analysis and SLAM mapping.

---

This README provides a detailed guide for setting up and launching the offline pipeline for radar data processing and mapping.
