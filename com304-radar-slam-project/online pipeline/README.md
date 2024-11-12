# Online Pipeline

This pipeline provides real-time mapping capabilities by combining radar data from the AWR1843BOOST radar and odometry from the Turtlebot 4. It includes nodes for radar data acquisition, transformation broadcasting, map generation, and visualization.

## Prerequisites

- Ensure you are connected to the Turtlebot 4 with the radar properly mounted and all necessary ROS2 packages installed on the Turtlebot.

## Steps to Run the Online Pipeline

### 1. Launch Radar Node

This node initializes the radar and begins streaming data to the ROS2 network.

- Open a terminal and connect to the Turtlebot 4 via SSH:
  - `ssh ubuntu@192.168.2.222`
  - Password: `turtlebot4`

- Set permissions for serial ports:
  - `ll /dev/serial/by-id`
  - `sudo chmod 666 /dev/ttyACM0`
  - `sudo chmod 666 /dev/ttyACM1`
  
  Wait for about 10 seconds to ensure the device is ready.

- Navigate to the radar ROS2 driver directory and launch the radar node:
  - `cd ~/mmwave_ti_ros/ros2_driver/src/ti_mmwave_rospkg/launch`
  - `ros2 launch 1843_Standard.py`

### 2. Launch Broadcaster Node

This node broadcasts transformations required to align radar data with the robot’s frame of reference.

- Open a new terminal and connect to the Turtlebot 4 via SSH:
  - `ssh ubuntu@192.168.2.222`
  - Password: `turtlebot4`

- Navigate to the broadcaster workspace and source the setup file:
  - `cd ~/broadcaster_ws/`
  - `. install/setup.bash`

- Launch the broadcaster node:
  - `ros2 launch tf_broadcaster tf_broadcaster.launch.py`

### 3. Launch Map Generation Node

This node generates a 2D occupancy map by projecting the radar’s 3D point cloud onto the ground plane.

- Open another terminal and connect to the Turtlebot 4 via SSH:
  - `ssh ubuntu@192.168.2.222`
  - Password: `turtlebot4`

- Navigate to the map generation workspace:
  - `cd ~/map_gen_ws/`

- Launch the map generation node:
  - `ros2 launch octomap_server2 octomap_server_launch.py`

### 4. Launch Visualization

Finally, visualize the robot's location and generated map using ROS visualization tools.

- On your local machine, launch the visualization node:
  - `ros2 launch turtlebot4_viz view_model.launch.py`

This will open the ROS visualization tool, where you can view the live occupancy map and track the Turtlebot's movements in real time.

---

Follow these steps in sequence to ensure smooth operation of the online pipeline. Each node performs a specific function critical to the SLAM pipeline, allowing you to visualize the real-time mapping of the environment.

---
