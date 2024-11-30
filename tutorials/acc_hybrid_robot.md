# Velocity-based WBC - Hybrid Robot

This tutorial assumes that you have installed [HyRoDyn](https://robotik.dfki-bremen.de/en/research/softwaretools/hyrodyn), and enabled the ROBOT_MODEL_HYRODYN option when you installed WBC. As of today (11/24) HyRoDyn is not openly available, so the installation requires an account on https://git.hb.dfki.de. 

The example can be found in [tutorials/rh5v2/rh5v2_hybrid.cpp](https://github.com/ARC-OPT/wbc/blob/master/tutorials/rh5v2/rh5v2_hybrid.cpp), documentation can be found [here](https://arc-opt.github.io/wbc/rh5v2__hybrid_8cpp.html). To run the tutorial, type
```
cd build/tutorials/rh5v2
./rh5v2_hybrid
```
The example shows velocity-based WBC on a hybrid dual-arm robot (fixed base). The outputs are the actuator velocities that comply with the given task space velocities. In contrast to the previous example, the solution respects the internal closed-loop mechanisms of the RH5v2 robot and is mapped directly to actuation space (see this [paper](https://arc-opt.github.io/Documentation/publications/icra_2022/index.html) for more details).

[[Previous Tutorial]](https://arc-opt.github.io/Documentation/tutorials/acc_serial_robot.html)[[Back to Main Page]](https://arc-opt.github.io/Documentation)[[Next Tutorial]](https://arc-opt.github.io/Documentation/tutorials/ros2_introduction.html)
