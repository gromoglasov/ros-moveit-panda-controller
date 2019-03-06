### Drawing on a Cartesian space using Panda Robot and ROS:

ROS package that automatically generates Cartesian space movements of the end-effector of the Panda robot manipulator: the end-effector "draws" squares of different sizes on the x-y Cartesian plane, starting from a given robot configuration.

### To run the package:

- Extract the package into your catkin workspace, if you do not have a catkin workspace, follow the following [link](https://wiki.ros.org/catkin/Tutorials/create_a_workspace)

- It is also assumed that you have MoveIt installed, if this is not the case, follow the following [link](https://docs.ros.org/kinetic/api/moveit_tutorials/html/doc/getting_started/getting_started.html) to install MoveIt

- First we need to download 2 repositories, which will allow to start rViz with the Panda robot model

- From your catkin workspace:

  ```shell
  git clone -b kinetic-devel https://github.com/ros-planning/moveit_tutorials.git
  git clone -b kinetic-devel https://github.com/ros-planning/panda_moveit_config.git
  ```

- Build your catkin workspace and source it by running:

  ```
  catkin build
  source ~/ws_moveit/devel/setup.bash
  ```

- After your workspace is ready, you need to make all of the nodes executable, run the following comands from the "scripts" folder containing all the nodes

  ```shell
  chmod +x square_size_generator.py
  chmod +x move_panda_square.py
  ```

- First we need to get roscore running:

  ```shell
  roscore
  ```

- In a separate terminal we can now launch the Rviz by running:

  ```
  roslaunch panda_moveit_config demo.launch
  ```

- In another terminal run the following:

  ```shell
  rosrun AR_week8_test square_size_generator.py
  ```

  This will initiate the first node, which generates a random square size and publishes it to the 'size' topic

- In a seperate terminal run the following:

  ```
  rosrun AR_week8_test move_panda_square.py
  ```

  This will initiate our main node, which subscribes to the 'size' topic, and communicates with the Panda Arm through MoveIt to 'draw' squares on a Cartesian plane

- To visulise the the joints positions, run: (add joint state positions 0-6 topics in the GUI)

- ```
  rosrun rqt_plot rqt_plot
  ```

### List of Dependencies:

- python 2.7
- catkin
- ros-kinetic
- rqt
- moveit_commander
- moveit_msgs