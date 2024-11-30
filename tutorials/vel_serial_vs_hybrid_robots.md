# Serial vs. Hybrid Robots

The tutorial can be found in the files [tutorials/rh5/rh5_single_leg.cpp](https://github.com/ARC-OPT/wbc/blob/master/tutorials/rh5/rh5_single_leg.cpp) and [tutorials/rh5/rh5_single_leg_hybrid.cpp](https://github.com/ARC-OPT/wbc/blob/master/tutorials/rh5/rh5_single_leg_hybrid.cpp), documentation can be found [here](https://arc-opt.github.io/wbc/rh5__single__leg_8cpp.html) and [here](https://arc-opt.github.io/wbc/rh5__single__leg__hybrid_8cpp.html).
To run the serial tutorial, type (for the serial robot):
```
cd build/tutorials/rh5
./rh5_single_leg
```
For the hybrid robot:
```
cd build/tutorials/rh5
./rh5_single_leg_hybrid
```

This tutorial assumes that you have installed hyrodyn and enabled the USE_HYRODYN option when you installed WBC. This will build the RobotModelHyrodyn class, which allows to specify WBC problems in the actuation space of series-parallel hybrid robot, i.e., robots with one or multiple parallel loops in their structure. Serial/tree-type models (like RobotModelKDL) will abstract parallel mechanism by the means of serial chains of rotational or prismatic joints. This has a number of disadvantages:
1) Box constraints describing the physical limitations of
the actuators within parallel submechanisms cannot be
considered in the optimization problem, which may
over- or under-estimate the admissible workspace of
the robot.
2) The parallel mechanisms may be subject to singularities that cannot be properly considered in the WBC.
3) The solution of the WBC problem will be less accurate.
as it does not capture the correct dynamics of the
parallel mechanisms.
4) It leads to custom and complicated robot control software stacks, which may be hard to maintain and reuse.

[[Previous Tutorial]](https://arc-opt.github.io/Documentation/tutorials/vel_floating_base_robots.html)[[Back to Main Page]](https://arc-opt.github.io/Documentation)[[Next Tutorial]](https://arc-opt.github.io/Documentation/tutorials/vel_serial_robot.html)
