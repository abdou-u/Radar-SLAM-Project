# Radar SLAM Project

## Overview

This project, conducted as part of the COM-304 course at EPFL, explores Simultaneous Localization and Mapping (SLAM) using mmWave radar technology. Our team utilized the AWR1843BOOST radar sensor combined with a Turtlebot 4 robot to develop a robust indoor SLAM system capable of performing in challenging environmental conditions. The project is split into offline and online pipelines, each focused on different aspects of SLAM implementation and optimization.

### Team Members
- [Ahmed Abdelmalek](https://people.epfl.ch/ahmed.abdelmalek)
- [Nestor Lomba](https://people.epfl.ch/nestor.lombalomba)
- [Jacopo Ferro](https://people.epfl.ch/jacopo.ferro)
- Andrew Wang

## Project Structure

The repository contains the following main folders:

- **com304-radar-slam-project**: Contains the final project report and supporting documents.
- **homework**: Includes Homework1.ipynb and Homework2.ipynb, which cover theoretical aspects like beamforming and matched filtering to build foundational knowledge for the project.
- **com304-radar-slam-project/offline pipeline**: Implements the offline SLAM pipeline, focusing on data preprocessing and mapping from radar raw data. This pipeline allows post-processing and model inference without real-time constraints.
- **com304-radar-slam-project/online pipeline**: The real-time implementation of SLAM, combining radar data and odometry from Turtlebot 4 to produce a live occupancy map of the environment.
- **com304-radar-slam-project/testing**: Includes various tests and benchmarks to validate and fine-tune our code. Each subdirectory contains a README with specific instructions on running tests.

## Project Goals and Motivation

Millimeter-wave radar provides several advantages over traditional sensors like LiDAR or cameras, including resilience in poor visibility conditions (e.g., fog, dust) and the ability to detect transparent materials. This project explores the potential of mmWave radar in indoor SLAM applications by leveraging its strengths for environmental perception and navigation.

### Key Objectives:
1. **Develop a SLAM system** that integrates radar and odometry data.
2. **Optimize radar parameters** for improved mapping accuracy.
3. **Overcome computational challenges** through a balanced offline and online approach.

## System Architecture

### 1. Hardware
The project employs the AWR1843BOOST radar sensor for environmental scanning and the Turtlebot 4 robot for mobility and odometry. The Turtlebot’s onboard processing and ROS2 compatibility make it ideal for real-time data synchronization and mapping.

### 2. Offline Pipeline
The offline pipeline is designed for in-depth data analysis and post-processing. Leveraging the [Radarize pipeline](https://github.com/ConnectedSystemsLab/xwr_raw_ros), it preprocesses radar data, performs noise reduction, and extracts features for SLAM mapping. Due to computational constraints, this pipeline does not run in real-time but is valuable for developing and testing mapping algorithms.

### 3. Online Pipeline
The online pipeline processes radar data in real-time using a ROS2-based setup. It integrates radar point clouds and Turtlebot odometry to build a dynamic occupancy map of the environment, suitable for real-time navigation and localization.

## Challenges and Solutions

Throughout the project, we encountered several technical challenges, including:

- **Hardware limitations**: The radar setup faced inconsistent performance and occasional data dropouts, which required troubleshooting and adaptation in data processing.
- **Software integration**: Compatibility issues between ROS2 (Ubuntu 22.04) and ROS1 components, as well as difficulties with the TI mmWave ROS2 driver, necessitated creative solutions to achieve seamless data flow.
- **Computational demands**: The need for GPU acceleration became apparent during data preprocessing, particularly for deep learning-based radar odometry estimation. This influenced our decision to focus on real-time SLAM using simpler techniques.

## Results

Our SLAM system achieved reliable indoor mapping using radar and odometry data. The generated occupancy maps demonstrated the potential of mmWave radar in environments where traditional sensors might struggle. The online pipeline successfully displayed live mapping results via ROS’s visualization tools, providing an intuitive view of the robot's surroundings.

## Future Work

To enhance this SLAM system, future work could focus on:

- **GPU acceleration**: Enabling real-time deep learning-based processing for radar data.
- **Sensor fusion**: Integrating radar data with LiDAR or camera inputs for a more comprehensive SLAM solution.
- **Dynamic SLAM**: Adapting the system for environments with moving objects.
- **Improved visualization**: Enhancing the user interface with advanced 3D mapping and augmented reality.

## Getting Started

### Prerequisites

- **ROS2**: The online pipeline uses ROS2 for real-time data handling and visualization.
- **Python**: The code includes several Python scripts for data processing.
- **AWR1843BOOST radar setup**: Ensure the radar is mounted and connected as described in the hardware setup section of our project report.

### Running the Pipelines

1. **Offline Pipeline**:
   - Navigate to the `offline pipeline` directory.
   - Refer to the README within this directory for specific setup and execution instructions.

2. **Online Pipeline**:
   - Navigate to the `online pipeline` directory.
   - Follow the instructions in the README to set up real-time data acquisition and map generation.

## References

For a complete list of references, please refer to the **Radar SLAM Report Paper** included in this repository.


---

