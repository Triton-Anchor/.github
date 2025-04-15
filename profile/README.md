# Welcome to TASK:
The Triton Anchor Software Kit

### Repositories:

[task_general](https://github.com/Triton-Anchor/General) contains no code and exists as a place to organize the deployment and development timeline.

[task_win_gui](https://github.com/Triton-Anchor/task_wingui) is the front-end location of the tool control software. It is built to run in windows, offer a responsive interface, and communicate with the rest of TASK's API.

<br />
All other repositories run in a Linux environemt (WSL) as ROS2 packages.
<br />

[task_core](https://github.com/Triton-Anchor/task_core)

[task_simulation](https://github.com/Triton-Anchor/task_simulation)
     
[task_logger](https://github.com/Triton-Anchor/task_logger)

[task_service](https://github.com/Triton-Anchor/task_service)

## Creating a TASK repository/package:

### Guidelines:
- Prepend package names with 'task_' for consistency and distinction from other ROS2 packages
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
Task nodes are all at their core ROS2 Lifecycle Nodes. The core repository defines low-level mix-ins that add functionality on top of the basic ROS2 lifecycle management.
When creating a new node, these mixins offer compatibility with the system. As all the mixins are useful in most cases, the 'TaskNode' module rolls everything together into one inheritable base class.
The mixins add properties as follows:

#### Remote Lifecycle Node
A remote lifecycle node listens to a ros service: 'NODE_NAME'/lifecycle to set the lifecycle state. This allows a manager to configure many or all nodes at once.

#### Bus Node
The name 'Bus Node' refers to a node that is connected to one of the four main data buses in the TASK architecture. These nodes are able to listen to a sub-set of published data topics and direct information to its workers. Each Bus Node has its own type of worker class that it can spawn instances from.

#### Bus Node Worker
Bus Node Workers (not true nodes) belong to Bus Nodes and are where the module-specific work happens for each node. The number of workers for a given node is tied directly to the number of modules connected.

As an example, the Data Aquisition Node is the node that aggregates all transmited data. If a 3x module tool is connected, the Data Aquisition Node will spawn three 'logger' workers to handle the binary data logging for each module.

#### State Config
As all core parameters are stored in yaml files, the State Config mixin contains methods that provide nodes with easy access to these contents. Message size, format, parameters, etc. are read into local variables with this mixin.

### Managers
To address the decentralized nature of a node-based architecture, the CCT (a special Node in task_core) offers a central location for getting and setting parameters that apply system wide. The CCT inherits special 'manager' versions of the listed mixins that allows it to set lifecycle states, notify bus nodes of new modules, and read in global state configurations.
