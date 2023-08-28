To run a simple Cartesian pose control example, you can do
`
ros2 launch wbc_ros cartesian_space_example.py
`
To visualize the robot, you can do 
`
rviz2 -d install/wbc_ros/share/wbc_ros/config/default.rviz
`
You should now see the KUKA iiwa robot in rviz performing a circular end effector trajectory. 



If you type `ros2 control list_controllers` you should the following available controller: 
