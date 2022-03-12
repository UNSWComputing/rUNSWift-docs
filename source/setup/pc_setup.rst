.. _pc_setup:

########
PC Setup
########

.. note::
    If this is your first time using rUNSWift software, follow the instructions on this page.
    For those that are looking to contribute to the codebase, please follow instructions on :ref:`pc-setup-contributing`.

******************
Install VirtualBox
******************

Download and Install `VirtualBox <https://www.virtualbox.org/wiki/Downloads>`_.

************************
Import rUNSWift VM Image
************************

#. Download OVA file from `http://robocup.web.cse.unsw.edu.au/runswift2/rUNSWift-VM.ova`
#. File -> Import Appliance
#. Select the Downloaded OVA file
#. Next
#. Import
#. Settings
    #. System
        * Motherboard
            =========== =======
            Base Memory 4096 MB
            =========== =======

            .. tip::
                Memory size of 2GB is a minimum.
                Recommendation is half your system memory.
        * Processor
            ============ ======
            Processor(s) 4 CPUs
            ============ ======

            .. tip::
                Maximum 1 CPU per 1.5GB Base Memory
                Recommendation is equal to the number of cores on your system.  Ignore the 'Invalid settings detected'.
#. Start

.. tip::
    OVA file is very big (>5GB), and you have to be on campus or a CSE student to download it.

.. tip::
    We have a smaller (3.2GB) OVA file for external users at `http://robocup.web.cse.unsw.edu.au/runswift2-htpasswd/rUNSWeenie.ova`.

.. note::
    For passwords, please :ref:`contact` us.


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
    In case you're unable to connect to a robot (i.e. `ssh <robotname>` doesn't work), try the following steps, proceeding to the next step if the one you tried doesn't work:
        #. Try `ssh <robotname>.local`.
        #. Try `ssh nao@<robot_ip_address>`
        #. If the error message from any of the above steps was something like `Name or service not known`, try `ping <robotname>.local`. If this doesn't work:
            #. Check that your PC is connected to the network by pinging the router for instance i.e. `ping <router_ip_address>`. This IP address can be found by checking the Network Settings -> IPv4 address or by running `ifconfig`.
            #. Confirm that the robot has the right IP address. (There might be a `button combo <https://runswift.readthedocs.io/en/latest/running/button_presses.html#chest-button-interface>`_ for this.)
            #. Check the router for the list of devices connected to it. The robot should appear as a wifi client or DHCP client(wired). This can be done by installing a network utility such as `nmap <https://nmap.org>`_.
            #. If you're connected via WiFi, try connecting via Ethernet(wired) and vice-versa.
        #. Try `avahi-browse -av` and check the output to see if the name of the robot you're connecting to is listed.
        #. Install `Wireshark <https://www.wireshark.org/download.html>`_ and monitor the packets to diagnose the issue. If you find this step overwhelming, please seek help from one of the more experienced members.
