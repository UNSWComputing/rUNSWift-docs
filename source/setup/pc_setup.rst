.. _pc_setup:

########
PC Setup
########

.. note::
    ⚠ ⚠ ⚠ This guide is probably so outdated it needs to be decommissioned. If you're here for rUNSWift Bootcamp, please follow
    the instructions you have been provided in Discord, not anything on this page.

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
    In case you're unable to connect to a robot (i.e. ``ssh <robotname>`` doesn't work), try installing `Wireshark <https://www.wireshark.org/download.html>`_ and monitoring the packets to diagnose the issue. 	Also try pinging by the expected IP address of the robot, ``ping <robotname>.local``, and checking the output of ``avahi-browse -av``.
