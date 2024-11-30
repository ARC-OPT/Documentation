[Code API](https://arc-opt.github.io/wbc/index.html)  | [WBC Library](https://github.com/ARC-OPT/wbc/)   | [WBC ROS](https://github.com/ARC-OPT/wbc_ros/) 

# Introduction

### Whole-Body Control

Whole Body Control (WBC) is an approach for specifying and controlling complex robotic tasks
[Synthesis and Control of Whole-Body Behaviors in Humanoid Systems](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.73.8747&rep=rep1&type=pdf).

<img src="images/wbc_principle.svg" alt="drawing" width="600"/>

Image Credits: Dennis Mronga, DFKI

The idea is to define a set of feedback controllers around an optimization problem. Each controller regulates a certain task, the control output is fed into the cost function of the optimization problem, typically a quadratic program, and thus minimized during execution.
In each control cycle ...
  * The cost function is updated with the current robot state and controller reference
  * The optimization problem is solved
  * The solution is applied to the actuators of the robot
  
WBC is used for...
 
  * controlling robots with redundant degrees of freedom, like humanoids or other legged robots with floating base, but also fixed-base systems like mobile manipulators, dual-arm systems or even simple manipulators. In general, the number of robot dof can be arbitrarily high like >50. 

  * controlling multiple tasks simultaneously while taking into account the physical constraints of the robot. E.g., on a humanoid robot do ... (1) keep balance (2) Grasp an object with one arm (3) maintaining an upright body posture (4) Consider the joint torque limits, etc... 

  * reactive robot control, i.e., it does not involve any motion planning or trajectory optimization. However, it can be used to stabilize trajectories coming from a motion planner or trajectory optimizer and integrate them with other objectives and physical constraints of the robot. Other than in MPC, the optimization horizon has the size 1, i.e., there is no prediction model involved. 

###  ARC-OPT: Motivation

ARC-OPT is a framework for optimization-based control of redundant robots. It contains various implementations of whole-body feedback control approaches on velocity-, acceleration- and force/torque-level. The core WBC library is written in C++, with Python bindings for most functionalities. It aims at facilitating the specification and benchmarking of whole-body controllers for redundant robots, i.e., the target user group are software developers and control engineers. Compared to existing frameworks for optimization-based robot control, ARC-OPT provides

 * A common interface to several WBC approaches on velocity, acceleration, and torque control level, using different solvers and robot models
 * A learning module that allows to automatically derive, adapt, and optimize WBC tasks (will made be open-source soon)
 * An approach for modeling and solving WBC problems on series-parallel hybrid robots, as described in [this paper](publications/icra_2022/index.html)  (will made be open-source soon)

###  Concepts

The design of WBC library separates the whole-body controller into 4 main building blocks, namely controller(s), robot model, scene and solver. Robot models, scenes and solvers are implemented as plugins, which can be exchanged.

![wbc_overview](images/wbc_overview.svg)

* **Controller**: A controller implements a task space function, e.g., maintain a certain contact force, follow a trajectory, or avoid an obstacle. Each controller can be designed either in task or joint space of the robot. Thus, depending on the implementation, the input of a controller can be a target pose, twist, or spatial acceleration (task space), as well as a joint position, velocity or acceleration (joint space). The control output, which is passed to the scene, describes the error of the task function, which is minimized during execution. All controllers are agnostic to the robot kinematics and dynamics, as well as the underlying WBC implementation. The available controllers can be found [here](https://github.com/ARC-OPT/wbc/tree/master/src/controllers).

* **Scene**: The scene sets up a [quadratic program (QP)](https://en.wikipedia.org/wiki/Quadratic_programming). Each scene has a set of **tasks**, which are defined as part of the cost function, and a set of **constraints**, which are the physical constraints of the robot. In each control cycle, the scene is updated with the current robot kinematics/dynamics and the control outputs of all tasks. The output of the scene is the QP. The available scenes can be found [here](https://github.com/ARC-OPT/wbc/tree/master/src/scenes). Each scene inherits from [core/Scene](https://github.com/ARC-OPT/wbc/blob/master/src/core/Scene.hpp).
  * **Task**: A task is essentially a summand in the cost function of the QP. The input of a task (task reference) is the control output of a controller. Thus, the control error is minimized by minimizing the cost function. Each task inherits from [core/Task](https://github.com/ARC-OPT/wbc/blob/master/src/core/Task.hpp) and is paramerized by [core/TaskConfig](https://github.com/ARC-OPT/wbc/blob/master/src/core/TaskConfig.hpp). There are currently three types of tasks: Joint Space tasks, Cartesian tasks, and CoM Tasks. Each scene can have an arbitrary number of tasks. 
  * **Task weights**: The importance of each task can be governed by either strict or soft priorities, where the latter are called task weights here. The solution of the QP will be a weighted sum of all task constributions, where tasks with higher tasks weights will be preferred.  task weight of zero means that the corresponding task variable will be ignored in the solution, e.g., a certain direction in tasks space. 
  * **Task priority**: In contrast to task weights, task priorities implement a strict task hierarchy, where tasks with lower priority will be executed in the [Nullspace](https://en.wikipedia.org/wiki/Kernel_(linear_algebra)) of the tasks with higher prioritiy. As a result, the task with highest priority will be executed first, the tasks with lower priority only if enough redundant DoF are available, and so on. Note that the only scene/solver combination that currently allows task prioritization is (velocity/hls).
  * **Joint Weights**: Similar as task weights, joint weights govern the importance of each joint in the solution. A joint weight of zero means that the joint will not be used at all. 
  * **Constraint**: Constraints describe the physical limitations of the robot and/or the environment, e.g., torque limits, ground friction or self-collisions. Each constraint inherits from [core/Constraint](https://github.com/ARC-OPT/wbc/blob/master/src/core/Constraint.hpp). Currently the constraints a hard-coded in the Scene implementation. Thus, if you want to use different constraints, you will have to implement a new Scene. 
* **Robot Model**: The robot model computes the kinematic and dynamic information that the scene requires to set up the optimization problem. This includes different Jacobians and their derivatives, frame transformations, gravity forces and torques, as well as mass-inertia matrices. The robot model is updated in each control cycle with the current joint status (position, velocity, acceleration) of the robot. Each robot model inherits from [core/RobotModel](https://github.com/ARC-OPT/wbc/blob/master/src/core/RobotModel.hpp). The available robot models can be found [here](https://github.com/ARC-OPT/wbc/tree/master/src/robot_models).
* **Solver**:  The solver is a generic component that solves a variant of a QP. The input is a QP, the output is a velocity, acceleration or torque command in configuration space of the robot. Each solver inherits from [core/QPSolver](https://github.com/ARC-OPT/wbc/blob/master/src/core/QPSolver.hpp). The available solver can be found [here](https://github.com/ARC-OPT/wbc/tree/master/src/solvers). 

# Installation
 * [WBC Library](installation/installation_no_rock.md)
 * [ROS 2 Interface](installation/installation_ros2.md)

# Testing

To execute unit tests for the WBC library, run
```
make test
```
from the library's build folder. This will execute unit tests for all installed components, e.g., solvers, robot models, etc.

# WBC Library Tutorials

### Velocity-based WBC
 
1. [Introductory example](tutorials/vel_introductory_example.md)
2. [Using a different solver](tutorials/vel_using_different_solver.md)
3. [Adapting task and joint weights](tutorials/vel_adapt_task_weights.md)
4. [Task hierarchies](tutorials/vel_task_hierarchies.md)
5. [Floating base robots](tutorials/vel_floating_base_robots.md)

### Serial vs. Hybrid Robots
  
5. [RH5 single leg example](tutorials/vel_serial_vs_hybrid_robots.md)
7. [RH5v2 dual arm serial](tutorials/acc_serial_robot.md)
8. [RH5v2 dual arm hybrid](tutorials/acc_hybrid_robot.md)

### Acceleration-based WBC

9. [Dynamic Cartesian Position Control](tutorials/acc_kuka_iiwa.md)

# ROS 2 Tutorials
1. [Introduction](tutorials/ros2_introduction.md)
2. [Cartesian Space Example](tutorials/ros2_cartesian_control.md)
3. [Joint Space Example](tutorials/ros2_joint_space_control.md)
4. [Nullspace Example](tutorials/ros2_nullspace_control.md)


# Publications

D. Mronga, S. Kumar and F. Kirchner, "[Whole-Body Control of Series-Parallel Hybrid Robots](publications/icra_2022/index.html)", 2022 International Conference on Robotics and Automation (ICRA), 2022, pp. 228-234

D. Mronga and F. Kirchner, "[Learning context-adaptive task constraints for robotic manipulation](https://www.sciencedirect.com/science/article/abs/pii/S0921889021000646?via%3Dihub)", Robotics and Autonomous Systems, Volume 141, 2021

D. Mronga, T. Knobloch, J. de Gea Fernández & F. Kirchner, "[A constraint-based approach for human–robot collision avoidance](https://www.tandfonline.com/doi/full/10.1080/01691864.2020.1721322?scroll=top&needAccess=true)", Advanced Robotics, Volume 34, Issue 5, pp. 265-281, 2020

D. Mronga, "[Learning Task Constraints for Whole-Body Control of Robotic Systems](https://media.suub.uni-bremen.de/handle/elib/5942)", PhD Thesis, 2022, University of Bremen
