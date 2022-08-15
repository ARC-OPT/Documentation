The tutorial can be found in [tutorials/kuka_iiwa/cart_pos_ctrl_qpoases.cpp](https://github.com/ARC-OPT/wbc/blob/master/tutorials/kuka_iiwa/cart_pos_ctrl_qpoases.cpp). Documentation can be found [here](https://arc-opt.github.io/wbc/cart__pos__ctrl__qpoases_8cpp.html).

This tutorial is identical to tutorial 01, except that we use a different solver (QPOases) and scene (VelocitySceneQuadraticCost) here. The main differences are:
* QPOases allows inequality constraints, e.g.., joint velocity limits, which is not possible with the HLS solver
* QPOases allows hard constraints, i.e., the constraints will never be violated. The HLS solver may return a sub-opotimal solution, which may violate the constraints
* The VelocitySceneQuadraticCost models the tasks in the cost functional, while the VelocityScene models them as constraints

### Use QPOases to limit the joint velocities

<video width="320" height="240" controls>
   <source type="video/mp4"  src="https://raw.githubusercontent.com/ARC-OPT/ARC-OPT/master/videos/tutorial_02.mp4"/>
</video>

In the video, again the upper plot shows the joint velocity of joint 4 (elbow), the lower plot shows the setpoint and actual position (only z-axis). As it can be seen the joint velocity of joint 4 is now bounded to the maximum joint velocity set in the URDF file (approx. 1.3 rad/s).
