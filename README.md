# dof6_demo_ws

ROS 2 workspace with a 6-DoF robot description, RViz visualization, and a `ros2_control` demo based on a mock hardware component.

## Requirements

- Ubuntu with ROS 2 installed
- Tested with ROS 2 Jazzy
- `colcon`, `xacro`, `rviz2`, `ros2_control`, and `rqt_joint_trajectory_controller`

If something is missing, install dependencies with:

```bash
source /opt/ros/$ROS_DISTRO/setup.bash
cd ~/dof6_demo_ws
rosdep install --from-paths src --ignore-src -r -y --rosdistro $ROS_DISTRO
```

If `rosdep` itself is not installed:

```bash
sudo apt update
sudo apt install python3-rosdep
```

## Build

```bash
source /opt/ros/$ROS_DISTRO/setup.bash
cd ~/dof6_demo_ws
colcon build --symlink-install
source install/setup.bash
```

## Launch Files

### 1. Visualization only

```bash
ros2 launch dof6_demo_description view_r6bot.launch.py
```

What it starts:

- `robot_state_publisher`
- `joint_state_publisher_gui`
- `rviz2`

Use this when you only want to inspect the URDF and move joints with sliders.

### 2. Control demo

```bash
ros2 launch dof6_demo_bringup r6bot_controller.launch.py
```

What it starts:

- `ros2_control_node`
- `robot_state_publisher`
- `joint_state_broadcaster`
- `r6bot_controller`
- `rviz2`
- `rqt_joint_trajectory_controller`

Use this when you want the robot running through `ros2_control` with the mock hardware backend.

## Difference Between the Two

- `view_r6bot.launch.py` is for visualization only.
- `r6bot_controller.launch.py` is for control, controllers, and trajectory testing.
- The second launch does not use the custom hardware plugin anymore. It uses `mock_components/GenericSystem`.

## Typical First Run

```bash
source /opt/ros/$ROS_DISTRO/setup.bash
cd ~/dof6_demo_ws
rosdep install --from-paths src --ignore-src -r -y --rosdistro $ROS_DISTRO
colcon build --symlink-install
source install/setup.bash
ros2 launch dof6_demo_description view_r6bot.launch.py
```

## Notes

- If a launch file is not found, make sure you ran `source install/setup.bash` in the current terminal.
- If you changed code or launch files, rebuild the workspace before launching again.
