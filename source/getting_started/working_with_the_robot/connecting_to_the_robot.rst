******************************
Connecting to the robot
******************************

.. warning::
    You only have to follow these steps if you have to connect to an actual robot.

First, run `make update-hosts`. This will update your hosts file with the robot 
names in your system so you can ssh with their names rather than their IPs. 

Next, put your ssh key in `image/home/nao/.ssh/authorized_keys`. Then sync with 
the robot or flash it (I think? Idk). Idk if our default password is meant to be
public information or not.

Make sure you're on the same network as the robot and the robot is visible. If 
connecting over LAN directly to robot, use 10.1.AA.2XX, where AA is the team code
and XX is any numbers between 0 and 54. For rUNSWift, AA is 18 and we use 2XX because
0 and 1 starting numbers are reserved for the robots. If connecting over wireless
without a router, use 10.0.AA.2XX. If you have a router, DHCP should be fine.
Typically we connect to a robot with ``ssh nao@<robotname>``. 