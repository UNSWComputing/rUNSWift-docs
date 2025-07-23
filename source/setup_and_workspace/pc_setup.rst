.. _pc_setup:

########
PC Setup
########

make setup 

make dev

We rely on some third party packages, and for more information on how 
those work, see those packages themselves. For a complete list of dependencies, 
workspace package dependencies are listed in
robot_ws/src/3rdparty/scripts/install-dependencies.sh, workspace dependencies are listed
in the dockerfile and robot dependencies are located in 
/firmware/naoimage-snippets.


.. _setup_network:

******************************
Setup Wireless/Wired Network
******************************

.. warning::
    You only have to follow these steps if you have to connect to an actual robot.


For a VM, it is necessary to bridge wireless networks and wired networks (when using LAN)
from the host machine to the VM. Follow these instructions in VirtualBox.

#. Network
    #. Adapter 2
        #. Enable Network Adapter
        #. Attached to Bridged Adapter
        #. Name should be your wired adapter
        
.. note::
    In case you're unable to connect to a robot (i.e. ``ssh <robotname>`` doesn't work), try installing `Wireshark <https://www.wireshark.org/download.html>`_ and monitoring the packets to diagnose the issue. 	Also try pinging by the expected IP address of the robot, ``ping <robotname>.local``, and checking the output of ``avahi-browse -av``.
