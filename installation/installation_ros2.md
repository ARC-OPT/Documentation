## Install using ROS 2

1. Install ROS 2 Humble as described [here](https://docs.ros.org/en/humble/Installation.html), base install + dev_tools are mimimum required
2. Install the WBC library as described [here](https://arc-opt.github.io/Documentation/installation/installation_no_rock.html)
3. If not yet done, init rosdep
   ```
   sudo rosdep init && rosdep update
   ```
4. Install wbc_ros packages
   ```
   mkdir -p ros2_ws/src
   cd ros2_ws
   vcs import src --input https://raw.githubusercontent.com/ARC-OPT/wbc_ros/main/repos.yaml
   rosdep install --from-paths src -i -r -y
   colcon build --symlink-install
   source install/setup.bash
   ```
   
[[Back to Main Page]](https://arc-opt.github.io/Documentation)
