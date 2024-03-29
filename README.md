# ROS_NOTE

## Install ROS


## After install ROS
### Build up an enviroment for operating program 
Because you need to operate code in ROS format, catkin_make is the common way to build a enviroment for ROS to read your program's file. So we often create enviroment folder called catkin_ws.  
### 1. mkdir -p ~/catkin_ws/src
### 2. cd ~/catkin_ws 
### 3. catkin_make
This will create an enviroment catkin_ws with three folder "build","devel" and "src".  
#### src: put all pkg(from github) you need to this folder, then back to "~/catkin_ws" and execute "catkin_make" (whenever you put one, you need to execute once). It let ROS detect how many pkg you have, so you can directly use rosrun or roslaunch to execute file in this pkg.

## Control Universal Robot 10
Run the following code:
### 1. roscore
### 2. roslaunch ur_modern_driver ur10_bringup.launch robot_ip:=$ROBOT_IP
(replace "$ROBOT_IP" to IP of ur10 or ur5 like 192.168.2.1)  
This step is to connect to the Universal robot.  
  
Problem: If you use Ubuntu16 and catkin_make ur_modern_driver, it will show error.  
So you need to modify ~/ur_modern_driver/src/ur_hardware_interface.cpp  
Open ur_hardware_interface.cpp and replace all "->hardware_interface" by "->type".
  
### 3. roslaunch ur10_moveit_config ur10_moveit_planning_execution.launch limited:=True
Start path planning software, and "limited:=True" constrain robot not to collide.

### 4. roslaunch ur10_moveit_config moveit_rviz.launch
Start rviz, virtualize simulation software.

### 5. rosrun pkg x.py
Then you can start to use python or c++ to control robot arm through MOVEIT library.  
(P.S. In this step, you have to use "chmod +x x.py" to make x.py follow ROS format.)

Example: http://docs.ros.org/indigo/api/moveit_tutorials/html/doc/pr2_tutorials/planning/scripts/doc/move_group_python_interface_tutorial.html  
And you can find the group name from "/ur5_moveit_config/config/ur5.srdf".(https://github.com/ros-industrial/universal_robot/blob/93ba9e5e7090d07ef1c610daa33aba2012100ace/ur5_moveit_config/config/ur5.srdf)
