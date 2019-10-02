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

#. Download OVA file from ``runswift2.cse.unsw.edu.au/rUNSWift-VM.ova``
#. File -> Import Appliance
#. Select the Downloaded OVA file
#. Next
#. Import
#. Start

.. tip::
    OVA file is very big (>5GB), you have to be connected to the SPL_R network in the lab.

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
