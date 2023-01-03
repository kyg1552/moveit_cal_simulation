Running MoveIt Calibration in simulation
========================================

### Available on Docker
If you prefer, you can skip the steps below and use the [Docker
image](https://hub.docker.com/repository/docker/jstechschulte/moveit_calibration_simulation)
instead.

### Avoid OpenCV 3.2
OpenCV 3.2, which is what ships with Ubuntu 18.04, has a buggy ArUco pose detection implementation. The instructions
below assume you have OpenCV 3.4 installed in `/usr/local/`. OpenCV 3.4 can be easily installed as follows:

    git clone https://github.com/RoboticsYY/opencv_deb_install.git
    sudo dpkg -i opencv_deb_install/OpenCV-3.4/OpenCV-3.4.5-x86_64-*

### Downloading and building MoveIt Calibration and simulation packages
If you haven't already, install `catkin`:

    sudo apt install ros-noetic-catkin python3-catkin-tools

The simulation also requires Gazebo:

    sudo apt install ros-noetic-gazebo-ros ros-noetic-gazebo-plugins ros-noetic-gazebo-ros-control \
      ros-noetic-joint-state-controller ros-noetic-position-controllers ros-noetic-joint-trajectory-controller

Set up a new workspace using the included `moveit_cal_simulation.rosinstall`:

    mkdir -p ~/catkin_ws/src
    cd ~/catkin_ws/src
    wstool init .
    wstool merge -t . https://raw.githubusercontent.com/kyg1552/moveit_cal_simulation/main/moveit_cal_simulation.rosinstall
    wstool update -t .
    rosdep install -y --from-paths . --ignore-src --rosdistro noetic

Configure and build:

    cd ~/catkin_ws
    sudo apt-get install ros-noetic-moveit*
    catkin_make
    roslaunch rb5_moveit_config demo.launch

From there, follow [the tutorial](https://ros-planning.github.io/moveit_tutorials/doc/hand_eye_calibration/hand_eye_calibration_tutorial.html).
