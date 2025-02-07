# Welcome to TASK:
The Triton Anchor Software Kit

<br />

This page links to repos that organize Triton Anchor's code and controls planning.
Also contained here are guidelines for adding to TASK: Repositories, Packages, and Nodes

<br />

[task_general](https://github.com/Triton-Anchor/General) contains documents and timelines relating to the development/deployment schedule 
     
[task_windows_ui](https://github.com/Triton-Anchor) is built to operate in windows, quickly and cleanly reflect tool states, and make requests to the rest of the Tool Control API

<br />

Other than task_General and task_windows_ui, all packages are run in a Linux environemt (WSL) as ROS2 packages.

<br />

[task_1x_simulator](https://github.com/Triton-Anchor) can be used to simulate serial input from the tool and test the holistic TASK pipeline
     
[task_1x_client](https://github.com/Triton-Anchor/task_1x_client) handles ___
     
[task_state_handler](https://github.com/Triton-Anchor) handles ___
     
[task_ui_server](https://github.com/Triton-Anchor) handles ___

<br />

## Terms:

## Guidelines for creating a new TASK package:
- Naming convention:
     - Always prepend description with 'task_' for uniform distinction from other ROS2 packages
     - Use snake_case: all lower case letters and with '_' as the primary delimeter
- Choose to use cpp or python exclusively for each package
- Should include files:
    - README.txt that includes instructions for running package in isolation

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
   git remote add origin [ssh_link]
   git branch -M main
   git add .
   git commit -m "First Commit"
   git push -u origin main
   ```


