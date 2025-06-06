# Welcome to TASK:
The Triton Anchor Software Kit

### File Structure:
TASK_HOME/
├─ back_end/
├─ simulation/
│  ├─ nX_simulator.py
├─ logs/
│  ├─ 0_log.bin
│  ├─ 1_log.bin
│  ├─ *_log.bin
├─ static/
│  ├─ css/
│  │  ├─ generated/
│  ├─ js/
│  │  ├─ generated/
├─ templates/
│  ├─ index.html
├─ monolith.py

## System Diagram:
                                                                                 
┌────────────────────────────────────┐         ┌────────────┐         ┌─────────┐
│                                    │         │            │         │         │
│          RaspberrytPi CM4          ├─────┐   │   Flask    ├────┐    │  .css   │
│                                    │     │   │            │    │    │         │
┌──────────┐─┌──────────┐─┌──────────┐     │   ┌────────────┐    │    ┌─────────┐
│          │ │          │ │          │     │   │            │    │    │         │
│ATmega2560│ │ATmega2560│ │ATmega2560│     │   │  Manager   │    │    │  .html  │
│          │ │          │ │          │     │   │            │    │    │         │
┌────┐┌────┐ ┌────┐┌────┐ ┌────┐┌────┐     │   ┌────────────┐    │    ┌─────────┐
│    ││    │ │    ││    │ │    ││    │     │   │            │    │    │         │
│ DRV││PSM │ │ DRV││PSM │ │ DRV││PSM │     └──►│  TCP sock  │    └───►│  .js    │
│    ││    │ │    ││    │ │    ││    │         │            │         │         │
└────┘└────┘ └────┘└────┘ └────┘└────┘         └────────────┘         └─────────┘



### Guidelines:
- Prepend package names with 'task_' for consistency
- snake_case: all lower case letters with '_' as the primary delimeter
- Include a README.md with instructions for running the package in isolation

### Process (Outdated):

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
