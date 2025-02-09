# Welcome to TASK:
The Triton Anchor Software Kit

<br />

This page links to repos that organize Triton Anchor's code and controls planning.
Also contained here are guidelines for adding to TASK: Repositories, Packages, and Nodes

<br />

[task_general](https://github.com/Triton-Anchor/General)
     
[task_windows_ui](https://github.com/Triton-Anchor)

<br />

Other than task_General and task_windows_ui, all packages run in a Linux environemt (WSL) as ROS2 packages.

<br />

[task_core](https://github.com/Triton-Anchor)

[task_1x_simulator](https://github.com/Triton-Anchor)
     
[task_1x_client](https://github.com/Triton-Anchor/task_1x_client)
     
[task_state_handler](https://github.com/Triton-Anchor)

[task_ui_server](https://github.com/Triton-Anchor)

<br />

## Terms:

## Steps for creating a new TASK package:

### Guidelines:
Prepend package name with 'task_' for uniform distinction from other ROS2 packages

snake_case: all lower case letters and with '_' as the primary delimeter

Choose to use cpp or python exclusively for each package

Include a README.md that includes instructions for running the package in isolation

### Process:

1. Create a new repo in github following the naming convention of other repos
2. In WSL enter a ros2 workspace src directory and create a new package with the SAME name as the repo using the ros2 pkg create build tool
   ```
   cd ~/ws/src

   # For python packages:
   ros2 pkg create --build-type ament_python <package_name>
   
   # For c++ packages:
   ros2 pkg create --build-type ament_cmake <package_name>
   ```
3. Build the package in the base directory
   ```
   cd ~/ws
   
   # If using a custom bash:
   rebuild
   
   # Otherwise:
   colcon build
   source install/setup.bash
   source /opt/ros/jazzy/setup.bash
   ```
4. In the package, initialize repo and link to the one made in github
   ```
   cd ~/ws/src/<package_name>
   
   git init
   git remote add origin <ssh_link>
   git branch -M main
   git add .
   git commit -m "First commit"
   git push -u origin main
   ```


