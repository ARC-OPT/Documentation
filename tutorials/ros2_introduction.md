WBC is integrated with [ros2_control](https://control.ros.org/master/index.html). The Whole-Body Controller itself, as well as every task space controller are implemented as [ros2 controllers](https://control.ros.org/master/doc/ros2_controllers/doc/controllers_index.html), inheriting from [ChainableControllerInterface](https://github.com/ros-controls/ros2_control/blob/master/controller_interface/include/controller_interface/chainable_controller_interface.hpp). 

## wbc_ros - Published Topics
* ```/whole_body_controller/solver_output``` - Solution provided by the qp solver
* ```/whole_body_controller/status_<task_name>``` - For each configured task (pose or joint state related to that task)
* ```/whole_body_controller/timing_stats``` - Computation times for different parts of the WBC

## wbc_ros - Subscribed Topics
* ```/whole_body_controller/task_activation``` - Activate (1) or deactivate (0) a task
* ```/whole_body_controller/task_weights``` - Set the task weights for individual task variables

## wbc_ros - Parameters
Check out the examples, e.g., [Cartesian Space Example](https://github.com/ARC-OPT/wbc_ros/blob/main/config/cartesian_space_example/iiwa_controllers.yaml)

