## Install using ROS 2

1. Install ROS 2 humble as described [here](https://docs.ros.org/en/humble/Installation.html), base install + dev_tools are mimimum required
2. Install the WBC library as described [here](https://arc-opt.github.io/Documentation/installation/installation_no_rock.html)
3. Create a ROS 2 workspace as described [here](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Creating-A-Workspace/Creating-A-Workspace.html) or use an existing one
4. If not yet done, init rosdep
   ```
   sudo rosdep init & rosdep update
   ```
5. Install wbc_ros packages
   ```
   cd ~/my_ros_workspace/src
   git clone https://github.com/ARC-OPT/wbc_msgs.git
   git clone https://github.com/ARC-OPT/wbc_ros.git
   cd ..
   rosdep install --from-paths src/wbc_ros -i src/wbc_msgs
   colcon build --symlink-install
   source install/setup.bash
   ```
   
[Back to Main Page](https://arc-opt.github.io/Documentation)
