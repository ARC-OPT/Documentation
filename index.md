# Documentation

### Whole-Body Control

Whole Body Control (WBC), also referred to as constraint-based or optimization-based control, is an approach for specifying and controlling complex robotic tasks. 
The term was coined by Luis Sentis in his work
[Synthesis and Control of Whole-Body Behaviors in Humanoid Systems](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.73.8747&rep=rep1&type=pdf).

<img src="images/wbc_principle.svg" alt="drawing" width="600"/>

Image Credits: Dennis Mronga, DFKI

The idea is to break down the overall control problem into multiple, simultaneously running tasks. A task in WBC is defined as a function in task space. The gradient of this task function will be minimized by the solver during execution. The tasks are specified as constraints or within the cost function of an online optimization problem, typically a quadratic program.
Now, in each control cycle ...
  * The constraints/cost function are updated with the current robot state/control reference
  * The optimization problem is solved
  * The solution is applied to the actuators of the robot
  
An advantage of this approach is that complex tasks can be composed from low-dimensional descriptors, which are typically  easier to specify and control than the complete task are once. Also, the redundancy of the robot is nicely exploited utilizing all the dof of the system (whole body). 

###  Intended Usage

WBC is a standalone library for optimization-based control of redundant robots. It contains various implementations of whole-body feedback control approaches on velocity-, acceleration- and force/torque-level. 

WBC is meant ...

  * for controlling robots with redundant degrees of freedom, like humanoids or other legged robots with floating base, but also fixed-base systems like mobile manipulators, dual-arm systems or even simple manipulators. In general, the number of robot dof can be arbitraryily high like >50. 

  * for controlling multiple tasks simultaneously while taking into account the physical constraints of the robot. E.g., on a humanoid robot do ... (1) keep balance (2) Grasp an object with one arm (3) maintaining an upright body posture (4) Consider the joint torque limits, etc... 

  * to be a purely reactive approach, i.e., it does not involve any motion planning or trajectory optimization. However, it can be used to stabilize trajectories coming from a motion planner or trajectory optimizer and integrate them with other objectives and physical constraints of the robot. 

The library is written in C++, with Python bindings for most functionalilities. It aims at facilitating the specification and benchmarking of whole-body controllers for redundant robots, i.e., the target user group are software developers and control engineers.


# Installation
 * [Using Rock](installation/installation_rock.md)
 * [Outside Rock](installation/installation_no_rock.md)

# Framework Overview
 * [WBC Library](framework/wbc_library.md)
 * [Rock Integration](framework/wbc_rock_integration.md)

# Tutorials

### Velocity-based WBC
 
1. [Introductory example](tutorials/vel_introductory_example.md)
2. [Using a different solver](tutorials/vel_using_different_solver.md)
3. [Adapting task and joint weights](tutorials/vel_adapt_task_weights.md)
4. [Task hierarchies](tutorials/vel_task_hierarchies.md)
5. [Serial vs. Hybrid robots](tutorials/vel_serial_vs_hybrid_robots.md)
6. [Floating base robots](tutorials/vel_floating_base_robots.md)

### Acceleration-based WBC
  
7. [Serial Robot](tutorials/acc_serial_robot.md)
8. [Hybrid Robot](tutorials/acc_hybrid_robot.md)

