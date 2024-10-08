# WBC ROS 2 - Joint Space Example

To run a simple Joint space example, you can do
```
ros2 launch wbc_ros joint_space_example.launch.py
```
Again, to visualize the robot, you can do 
```
rviz2 -d install/wbc_ros/share/wbc_ros/config/default.rviz
```
You should now see the KUKA iiwa robot in rviz, performing a trajectory in joint space. 

<img src="https://github.com/ARC-OPT/Documentation/assets/8993546/1be0a0a5-d2f4-469d-b792-c5b04b6ce361" alt="rviz2" width="400"/>
<br/>
<br/>

In the [joint_space_example.launch.py](https://github.com/ARC-OPT/wbc_ros/blob/main/launch/joint_space_example.launch.py) file, the code to load the example is explained step by step. This [iiwa_controllers.yaml](https://github.com/ARC-OPT/wbc_ros/blob/main/config/joint_space_example/iiwa_controllers.yaml) file describes the ROS 2 control configuration, which is loaded in the launch file. 

If you type `ros2 control list_controllers` you can see the available controllers: 
```!bash
whole_body_controller[wbc_ros/WholeBodyController] active    
joint_state_broadcaster[joint_state_broadcaster/JointStateBroadcaster] active    
joint_position_controller[wbc_ros/JointPositionController] active
```

[[Previous Tutorial]](https://arc-opt.github.io/Documentation/tutorials/ros2_cartesian_control.html)[[Back to Main Page]](https://arc-opt.github.io/Documentation)[[Next Tutorial]](https://arc-opt.github.io/Documentation/tutorials/ros2_nullspace_control.html)
