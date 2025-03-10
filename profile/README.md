# Welcome to TASK:
The Triton Anchor Software Kit

### Repositories:

[task_general](https://github.com/Triton-Anchor/General) contains no code and exists as a place to organize the deployment and development timeline.

[task_windows_ui](https://github.com/Triton-Anchor) is the front-end location of the tool control software. It is built to run in windows, offer a responsive interface, and communicate with the rest of TASK's API.

<br />
All other repositories run in a Linux environemt (WSL) as ROS2 packages.
<br />

[task_core](https://github.com/Triton-Anchor)

[task_1x_simulator](https://github.com/Triton-Anchor)
     
[task_state_manager](https://github.com/Triton-Anchor/task_state_manager)

## Creating a TASK repository/package:

### Guidelines:
- Prepend package name with 'task_' for consistency and distinction from other ROS2 packages
- snake_case: all lower case letters with '_' as the primary delimeter
- Choose beforehand to use cpp or python exclusively for each package
- Include a README.md with instructions for running the package in isolation

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
4. Initialize a new repo and link it to the one made in github
   ```
   cd ~/ws/src/<package_name>
   
   git init
   git remote add origin <ssh_link>
   git branch -M main
   git add .
   git commit -m "First commit"
   git push -u origin main
   ```
   
## Creating a TASK node:

