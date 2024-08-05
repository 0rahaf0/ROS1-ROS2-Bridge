# ROS1-ROS2-Bridge
This repository contains detailed instructions and necessary files to create a bridge between ROS1 (Noetic) and ROS2 (Foxy). This bridge allows communication between ROS1 and ROS2 nodes, enabling seamless integration between the two versions.

## Prerequisites

- Ubuntu 20.04
- ROS1 Noetic installed
- ROS2 Foxy installed
- `colcon` build tool installed

## Initialize ROS Workspaces

-ROS1 Workspace
mkdir -p ~/ros1_ws/src
cd ~/ros1_ws
catkin_make
source /opt/ros/noetic/setup.bash

-ROS2 Workspace
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
colcon build
source /opt/ros/foxy/setup.bash

## Install Dependencies
-Navigate to the bridge workspace and install necessary dependencies:
cd ~/ros1_bridge_ws
rosdep install --from-paths src --ignore-src -r -y

## Build the ROS1-ROS2 Bridge
-Source the ROS2 environment and build the bridge workspace:
source /opt/ros/foxy/setup.bash
cd ~/ros1_bridge_ws
colcon build --symlink-install

## Source the Workspace
-Source the workspace to overlay it with the existing ROS2 environment:
source ~/ros1_bridge_ws/install/setup.bash

## Run the Bridge
-To run the bridge, open two separate terminals: one for ROS1 and one for ROS2.

-ROS1 Terminal
source /opt/ros/noetic/setup.bash

-ROS2 Terminal
source /opt/ros/foxy/setup.bash
source ~/ros1_bridge_ws/install/setup.bash
ros2 run ros1_bridge dynamic_bridge


## Additional Information
-Ensure that no ROS1 environment variables are set when sourcing ROS2. You can manually unset them if necessary:
unset ROS_DISTRO
unset ROS_PACKAGE_PATH
unset ROS_ROOT
unset ROS_MASTER_URI
unset ROS_PYTHON_VERSION
unset ROS_VERSION
-Use separate terminals for ROS1 and ROS2 to avoid conflicts.

## Troubleshooting

-If you encounter any issues, please check the following:
Ensure all dependencies are installed.
Ensure that the correct environment variables are sourced for each ROS version.
Check for any residual ROS1 environment variables when sourcing ROS2.
