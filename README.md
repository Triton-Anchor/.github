# Welcome to TASK:
Triton Anchor Software Kit

## Terms:

## This page contains links to (n) repos that organize Triton Anchor's code and controls planning.
1. task_General        - General repo that contains documents and timelines relating to the development/deployment schedule 
2. task_windows_ui     - Front-end UI code block. Built to operate in windows, quickly and cleanly reflect tool states and make requests to the rest of the Tool Control API
3. task_1x_simulator   -
4. task_1x_client      -
5. task_state_handler  - 
6. task_ui_server      -

## Guidelines for creating a new TASK package:
Other than task_General and task_windows_ui, all packages should be made to run in Linux as ROS2 packages.
Triton Anchor Software Kit -> Ros Package
These packages/repos are made to support better organization of this distributed software kit.  

- Should include nodes necessary to be runable and testable in isolation
- Choose to use cpp or python exclusively each package

- Should include files:
    - README.txt
    - test script/node
