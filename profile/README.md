# Welcome to TASK:
The Triton Anchor Software Kit

This page links to repos that organize Triton Anchor's code and controls planning.
Also contained here are guidelines for adding to TASK: Repositories, Packages, and Nodes

[task_General](https://github.com/Triton-Anchor/General)
     General repo that contains documents and timelines relating to the development/deployment schedule 
     
[task_windows_ui](https://github.com/Triton-Anchor)
     Front-end UI code block. Built to operate in windows, quickly and cleanly reflect tool states and make requests to the rest of the Tool Control API
     
[task_1x_simulator](https://github.com/Triton-Anchor)
     Description
     
[task_1x_client](https://github.com/Triton-Anchor/task_1x_client)
     Description
     
[task_state_handler](https://github.com/Triton-Anchor)
     Description
     
[task_ui_server](https://github.com/Triton-Anchor)
     Description

## Terms:

## Guidelines for creating a new TASK package:
Other than task_General and task_windows_ui, all packages should be made to run in Linux as ROS2 packages.
Triton Anchor Software Kit -> Ros Package
These packages/repos are made to support better organization of this distributed software kit.  

- Should include nodes necessary to be runable and testable in isolation
- Choose to use cpp or python exclusively each package
- Naming convention:
     Always prepend description with 'task_' for uniformity (ex: task_<description>)
     Use all lowercase letters
     Use '_' as the primary delimeter

- Should include files:
    - README.txt
    - test script/node

## Steps for creating a new TASK package:
1. Create a new repo in github following the naming convention of other repos
2. In WSL enter a ros2 workspace src directory and create a new package with the SAME name as the repo using the ros2 pkg create build tool
   ```
   cd ~/ws/src
   
   # For python packages:
   ros2 pkg create --build-type ament_python <package_name>
   
   # For c++ packages:
   ros2 pkg create --build-type ament_cmake <package_name>
   ```
3. Navigate back to the base directory and build the package
   ```
   cd ~/ws
   
   # If using a custom bash:
   rebuild
   
   # Otherwise:
   colcon build
   source install/setup.bash
   source /opt/ros/jazzy/setup.bash
   ```
4. Create and link a git repo to one made in github
   ```
   git init
   git remote add origin <repo_name>
   git fetch
   git checkout origin/master -ft
   ```


