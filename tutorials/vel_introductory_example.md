# Introductory Example

WBC is a C++ library for task-oriented control of redundant robots. It facilitates the specification of different whole-body control approaches. The inputs of a whole-body controller are given as trajectories in task space (e.g., target pose, twist and acceleration), each of which corresponds to a different control objective. The output of the controller is the desired joint space velocity, acceleration or torque that is required to fulfill all the given objectives, under consideration of the physical constraints of the robot.

The whole-body controller consists of 4 major components, a set of controllers, the WBC scene, the robot model, and, the solver. 
In order to demonstrate how the components are specified, we develop a simple example.

## Cartesian position control on a 7-DOF arm

This tutorial can be found in [tutorials/kuka_iiwa/cart_pos_ctrl_hls.cpp](https://github.com/ARC-OPT/wbc/blob/master/tutorials/kuka_iiwa/cart_pos_ctrl_hls.cpp), documentation can be found [here](https://arc-opt.github.io/wbc/cart__pos__ctrl__hls_8cpp.html). To run the tutorial do
```
cd build/tutorials/kuka_iiwa
./cart_pos_ctrl_hls
```


<video width="320" height="240" controls>
   <source type="video/mp4"  src="https://raw.githubusercontent.com/ARC-OPT/ARC-OPT/master/videos/tutorial_01.mp4"/>
</video>


In the video, the upper plot shows the joint velocity of joint 4 (elbow), the lower plot shows the setpoint and actual position (only z-axis).

[[Back to Main Page]](https://arc-opt.github.io/Documentation)[[Next Tutorial]](https://arc-opt.github.io/Documentation/tutorials/vel_using_different_solver.html)
