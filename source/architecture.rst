############
Architecture
############

The ``runswift`` infrastructure is fairly large, so this page lists some
key aspects and summaries. The best way to understand these in detail is
to read the reference papers and relevant code.

ROS2
----

We run ROS2 Humble on ubuntu based on the image provided by Nao Devils:
https://github.com/NaoDevils/NaoImage.git

We have many packages within the codebase. Below is a quick summary of the main ones.
- **3rdparty**: Contains all 3rd party dependencies
- **behaviours**: Logic for the behaviours running on the robot
- **bringup**: Has higher level launch files for other packages
- **comms**: For communications from the robots to other robots and GameController
- **hri**: Human Robot Interaction; LEDs, buttons, touch sensors, speakers, etc.
- **kinematics**: Robot kinematics information
- **motion**: Robot movement
- **runswift_interfaces**: Interfaces for msgs between modules
- **stateestimation**: Robot localisation and ball tracking
- **vision**: Camera processing

Configuration
-------------

We have many ways to configure the way things run on the robot, and we try to 
follow the ROS2 pattern as closely as possible.

Parameters
~~~~~~~~~~


Launch files
~~~~~~~~~~~~

we have launch files.

Configs
~~~~~~~
The legacy way of using configs for each robot was to use .cfg files. We have 
not yet got around to moving to proper ROS2 ways of doing this and instead read 
in parameters from the config files as they were in legacy. The top level is 
`runswift.cfg <../tree/master/image/home/nao/data/runswift.cfg>`__, with
per-robot configuration files in the 
`robot.cfg <../tree/master/image/home/nao/data/configs>__`, or the robot body 
config `robot.cfg <../tree/master/image/home/nao/data/configs/body>__`. Our 
implementation was fairly inconsistent as we are probably going move to a more 
ROS2 like way of doing things, so make sure to check the launch files for which
file takes precedence for each parameter.


Running Architecture
--------------------

By default, we want the code to be running on boot because we want it to be game
ready. To make sure this happens, follow the instructions HERE? (readme)

Currently, we don't have any thread restarting logic as we were tight on time.
This is good for writing new code and debugging because you can see if it crashes
easily. However, if anyone reading this wants to implement it, read the 2024
Threads section LINK LINK LINKs



Logging
~~~~~~~

We have a cout-like interface for recording log messages to a file. For
example:

``llog(INFO) << "RUNSWIFT soccer library spinning up!" << endl;``

Log files are saved in /var/volatile/runswift on the robot, and there is
one log file per source directory. The log levels available are SILENT,
QUIET, FATAL, ERROR, WARNING, INFO, VERBOSE, DEBUG1, DEBUG2, and DEBUG3.
Setting a log level will record messages of that level or higher. The
default log level is SILENT, and can be overridden using one of the
options mechanisms listed in the options section. e.g. "-l INFO" will
record messages at level SILENT, QUIET, FATAL, ERROR, WARNING, or INFO.
Using llog (especially in tight loops) takes resources, even if the set
log level is higher (e.g. "-l SILENT") than the one passed to llog (e.g.
"llog(DEBUG3)").



