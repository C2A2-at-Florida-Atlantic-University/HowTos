██████╗  ██████╗ ███████╗    ███╗   ███╗███████╗██╗      ██████╗ ██████╗ ██╗ ██████╗
██╔══██╗██╔═══██╗██╔════╝    ████╗ ████║██╔════╝██║     ██╔═══██╗██╔══██╗██║██╔════╝
██████╔╝██║   ██║███████╗    ██╔████╔██║█████╗  ██║     ██║   ██║██║  ██║██║██║     
██╔══██╗██║   ██║╚════██║    ██║╚██╔╝██║██╔══╝  ██║     ██║   ██║██║  ██║██║██║     
██║  ██║╚██████╔╝███████║    ██║ ╚═╝ ██║███████╗███████╗╚██████╔╝██████╔╝██║╚██████╗
╚═╝  ╚═╝ ╚═════╝ ╚══════╝    ╚═╝     ╚═╝╚══════╝╚══════╝ ╚═════╝ ╚═════╝ ╚═╝ ╚═════╝
                                                                                                           
╦┌┐┌┌─┐┌┬┐┌─┐┬  ┬  ┌─┐┌┬┐┬┌─┐┌┐┌
║│││└─┐ │ ├─┤│  │  ├─┤ │ ││ ││││
╩┘└┘└─┘ ┴ ┴ ┴┴─┘┴─┘┴ ┴ ┴ ┴└─┘┘└┘

To install ROS Melodic.

To use ROS, you need to:
1. add the source from url
2. set up the key
3. install ROS
4. set up the ROS enviroment
5. initialize the ROS enviroment
6. create a ROS workspace
7. build the ROS workspace
8. install ROS packages
9. set up the network (if any).

Most of these steps you will only do once. The ones you will do often are related to installing ROS pacakges and building your workspace. Everytime a package is added or modified, you must build the workspace again.

*** Set up sources.list ***
$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list' # Add source url

*** Set up keys ***
$ sudo apt install curl # Install curl
$ curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add - # Download and add key

*** Install Melodic Full Desktop and dependencies ***
$ sudo apt install ros-melodic-desktop-full ros-melodic-catkin python-catkin-tools python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential

*** Set up enviroment ***
$ echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc # Append cmd source to load enviroment
$ source ~/.bashrc # Run .bashrc

*** Initialize enviroment ***
$ sudo rosdep init # To initialize it.
$ rosdep update # Update to latest

*** Create and Build a workspace ***
Choose your own <name_of_workspace> (catkin_ws is traditonal). We chose to use catkin_tools instead of the default catkin_make because it is better.*
$ mkdir -p ~/<name_of_workspace>/src/ # Make workspace folder
$ cd ~/<name_of_workspace>/ # Enter folder
$ catkin init # Init catkin workspace
$ catkin create pkg dummy_pkg # Dummy package to build workspace
$ catkin list # Check for all packages, should show only dummy
$ catkin build # Build workspace
$ echo "source ~/<name_of_workspace>/devel/setup.bash" >> ~/.bashrc # Add cmd to load space
$ source ~/.bashrc # Run .bashrc

To add support for Python 3, execute:
$ sudo apt install python3-dev python3-numpy python3-pip python3-yaml
$ pip3 install rospkg catkin_pkg
$ catkin config -DPYTHON_EXECUTABLE=/usr/bin/python3 -DPYTHON_INCLUDE_DIR=/usr/include/python3.6m -DPYTHON_LIBRARY=/usr/lib/x86_64-linux-gnu/libpython3.6m.so
$ export ROS_PYTHON_VERSION=3

*** Set up Network ***
Using any text editor (vi, vim, emac, gedit, nano, ...), edit .bashrc
$ sudo gedit ~/.bashrc

Change the following lines where <ip_master> is ROS Master's IP (Main Computer) and <ip_agent> is the IP of the current machine. When configuring ROS Master, both IPs are the same. If only one computer, leave as localhost.
> export ROS_MASTER_URI=http://<ip_master>:11311
> export ROS_HOSTNAME=<ip_agent>
$ source ~/.bashrc

EXAMPLE FOR A MASTER AND 1 ROBOT

+--------------------------------------------------+--------------------------------------------------+
|                    ROS MASTER                    |                      AGENT 1                     |
+--------------------------------------------------+--------------------------------------------------+
| > export ROS_MASTER_URI=http://<ip_master>:11311 | > export ROS_MASTER_URI=http://<ip_master>:11311 |
| > export ROS_HOSTNAME=<ip_master>                | > export ROS_HOSTNAME=<ip_agent_1>               |
+--------------------------------------------------+--------------------------------------------------+

╔═╗┌─┐┌─┐┬┌─┌─┐┌─┐┌─┐┌─┐
╠═╝├─┤│  ├┴┐├─┤│ ┬├┤ └─┐
╩  ┴ ┴└─┘┴ ┴┴ ┴└─┘└─┘└─┘
 
*** Install Turtlebot 3 packages ***
$ echo "export TURTLEBOT3_MODEL=waffle_pi" >> ~/.bashrc
$ sudo gedit ~/.bashrc
$ sudo apt install ros-melodic-dynamixel-sdk ros-melodic-turtlebot3-msgs ros-melodic-turtlebot3
$ cd ~/<name_of_workspace>/src
$ git clone -b melodic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git

*** Install ROS-NetSim Package (Python3 required) ***
$ cd ~/<name_of_workspace>/src
$ git clone https://github.com/alelab-upenn/ros-net-sim
$ cd ~/<name_of_workspace>
$ source /opt/ros/melodic/setup.bash
$ rosdep install -i --from-paths . -y
$ pip3 install empy
$ catkin init
$ catkin build


╔╗╔┌─┐┌┬┐┌─┐┌─┐
║║║│ │ │ ├┤ └─┐.
╝╚╝└─┘ ┴ └─┘└─┘.
* The main difference between catkin_tools and catkin_make is that catkin_tools provides an isolated environment that you get with:
$ catkin build

This makes the whole build configuration much more compartmentalized and robust to changes in the configuration (add/remove package, modify a cmake variable etc.)
In addition, building is done for independent packages in parallel which can make it much faster. Commands can be run at any path, not just the workspace root. It is easy to only build a single package (+ dependencies)
$ catkin build package_name # or, when called from the package directory
$ catkin build --this # Add <--no-deps> to skip dependencies.

You also get much better and easily-readable colored cmdline output which makes the whole experience much more pleasant.
Moreover, you also get many other useful subcommands with catkin including:
$ catkin clean # for cleaning the build, devel and install spaces
$ catkin list
$ catkin locate
$ catkin profile
See https://catkin-tools.readthedocs.io/en/latest/migration.html for more details
