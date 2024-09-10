# WBC ROS 2 - Nullspace Example

To run a nullspace example, you can do
```
ros2 launch wbc_ros nullspace_example.launch.py
```
Again, to visualize the robot, you can do 
```
rviz2 -d install/wbc_ros/share/wbc_ros/config/default.rviz
```
You should now see the KUKA iiwa robot in rviz. The robot maintains a fixed end effector pose, while moving the elbow joint along a trajectory. 

<img src="https://github.com/ARC-OPT/Documentation/assets/8993546/1be0a0a5-d2f4-469d-b792-c5b04b6ce361" alt="rviz2" width="400"/>
<br/>
<br/>

In the [nullspace_example.launch.py](https://github.com/ARC-OPT/wbc_ros/blob/main/launch/null_space_example.launch.py) file, the code to load the example is explained step by step. This [iiwa_controllers.yaml](https://github.com/ARC-OPT/wbc_ros/blob/main/config/null_space_example/iiwa_controllers.yaml) file describes the ROS 2 control configuration, which is loaded in the launch file. 

If you type `ros2 control list_controllers` you can see the available controllers: 
```!bash
joint_state_broadcaster[joint_state_broadcaster/JointStateBroadcaster] active    
whole_body_controller[wbc_ros/WholeBodyController] active    
ee_pose_controller  [wbc_ros/CartesianPositionController] active    
elbow_pose_controller[wbc_ros/CartesianPositionController] active
```
Here, the end effector task has a higher priority (0) than the elbow task (1). 

[[Previous Tutorial]](https://arc-opt.github.io/Documentation/tutorials/ros2_joint_space_control.html)[[Back to Main Page]](https://arc-opt.github.io/Documentation)
