# Velocity-based WBC - Serial Robot

The example can be found in [tutorials/rh5v2/rh5v2.cpp](https://github.com/ARC-OPT/wbc/blob/master/tutorials/rh5v2/rh5v2.cpp), documentation can be found [here](https://arc-opt.github.io/wbc/rh5v2_8cpp.html). To run the tutorial, type
```
cd build/tutorials/rh5v2
./rh5v2
```

This example shows velocity-based WBC on a serial dual-arm robot (fixed base). The outputs are the independent joint velocities that comply with the given task space velocities. The tasks are (1) to keep one arm at a fixed position, while (2) following a sinusoidal trajectory with the left arm. The robot's torso joints are thereby used to exploit the redundancy of the robot.

[[Previous Tutorial]](https://arc-opt.github.io/Documentation/tutorials/vel_serial_vs_hybrid_robots.html)[[Back to Main Page]](https://arc-opt.github.io/Documentation)[[Next Tutorial]](https://arc-opt.github.io/Documentation/tutorials/vel_hybrid_robot.html)
