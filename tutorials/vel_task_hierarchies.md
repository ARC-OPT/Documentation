# Task hierarchies

The example can be found in [tutorials/kuka_iiwa/cart_pos_ctrl_hls_hierarchies.cpp](https://github.com/ARC-OPT/wbc/blob/master/tutorials/kuka_iiwa/cart_pos_ctrl_hls_hierarchies.cpp), documentation can be found [here](https://arc-opt.github.io/wbc/cart__pos__ctrl__hls__hierarchies_8cpp.html). To run the tutorial, type
```
cd build/tutorials/kuka_iiwa
./cart_pos_ctrl_hls_hierarchies
```

### Implementation of Task Hierarchies

Fixed joint 5 position on highest priority:<br>
<video width="320" height="240" controls>
   <source type="video/mp4"  src="https://raw.githubusercontent.com/ARC-OPT/ARC-OPT/master/videos/task_hierarchies_1.mp4"/>
</video>
Fixed joint 5 position on lower priority:<br>
<video width="320" height="240" controls>
   <source type="video/mp4"  src="https://raw.githubusercontent.com/ARC-OPT/ARC-OPT/master/videos/task_hierarchies_2.mp4"/>
</video>

Please note that the visualization has been done with an external tool and is not part of ARC-OPT. If you want to visualize your system, please refer to the [ROS 2 tutorials](https://arc-opt.github.io/Documentation/tutorials/ros2_introduction.html), which use rviz as visualization.

[[Previous Tutorial]](https://arc-opt.github.io/Documentation/tutorials/vel_adapt_task_weights.html)[[Back to Main Page]](https://arc-opt.github.io/Documentation)[[Next Tutorial]](https://arc-opt.github.io/Documentation/tutorials/vel_floating_base_robots.html)


