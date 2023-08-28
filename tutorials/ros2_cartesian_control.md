To run a simple Cartesian pose control example, you can do
```
ros2 launch wbc_ros cartesian_space_example.py
```
To visualize the robot, you can do 
```
rviz2 -d install/wbc_ros/share/wbc_ros/config/default.rviz
```
You should now see the KUKA iiwa robot in rviz performing a circular end effector trajectory:

![Screenshot](https://github.com/ARC-OPT/Documentation/assets/8993546/1be0a0a5-d2f4-469d-b792-c5b04b6ce361)

If you type `ros2 control list_controllers` you should the following available controller: 
