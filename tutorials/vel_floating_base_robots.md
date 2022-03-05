The example can be found in [examples/rh5/rh5_legs_floating_base.cpp](https://github.com/ARC-OPT/wbc/blob/master/tutorials/rh5/rh5_legs_floating_base.cpp), documentation can be found [here](https://arc-opt.github.io/wbc/rh5__legs__floating__base_8cpp.html).

Here, we use the KDL-based robot model and configure a floating base, i.e.,  a 6 dof virtual linkage, which attaches the robot base to the world frame. Note that the robot is underactuated in this case, as we can only control the floating base joints indirectly by controlling the feet contacts with the ground.
