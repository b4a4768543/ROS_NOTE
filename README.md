# ROS_NOTE

## Install ROS


### After install ROS
## Control Universal Robot 10
Run the following code:
### 1. roscore
### 2. roslaunch ur_modern_driver ur10_bringup.launch robot_ip:=$ROBOT_IP
This step is to connect to the Universal robot.  
(roslaunch -> pkg -> file -> replace "$ROBOT_IP" to IP of ur10 or ur5 like 192.168.2.1)  
  
Problem: If you use Ubuntu16 and catkin_make ur_modern_driver, it will show error.  
So you need to modify ~/ur_modern_driver/src/ur_hardware_interface.cpp  
Open ur_hardware_interface.cpp and replace all hardware_interface by type.
  
### 3. roslaunch ur10_moveit_config ur10_moveit_planning_execution.launch limited:=True
Start path planning software, and limited constrain that robot do not have collision

### 4. roslaunch ur10_moveit_config moveit.rviz
Start rviz(virtualize simulation software)

### 5. rosrun pkg x.py
Then you can start to use python or c++ to control robot arm through MOVEIT library.  
(P.S. In this step, you have to use "chmod +x x.py" to make x.py follow ROS format.)

/ur5_moveit_config/config/ur5.srdf
