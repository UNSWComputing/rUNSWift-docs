.. _pc-setup:

########
PC Setup
########

These are setup instructions for contributing members of the team to setup their PC.
We use docker, so it should work on any system that can install docker. If you want,
you can use bare metal ubuntu or a vm but docker is recommended.

******************
Cloning Repository
******************

Run the following commands to clone the rUNSWift repository

.. code-block:: bash

   $ sudo apt-get install git
   $ git clone git@github.com:UNSWComputing/rUNSWift.git rUNSWift

.. note::
    Your GitHub account must have access to the private rUNSWift repository to be able to clone it. To gain access, please :ref:`contact` us.

******
Docker
******

The recommended way of setting everything up is just using the docker image
clone
run ``make dev``
voila, everything is set up.

*******************
Docker alternatives
*******************

Docker is great and runs on all platforms, but we have some instructions  TODO
vms work too

.. toctree::
    pc_setup_dual_boot
    pc_setup_linux
    pc_setup_wsl

***********************
Build Environment Setup
***********************

Run the following command to setup the build environment.

.. code-block:: bash

   $ make setup


.. note::
    For passwords, please :ref:`contact` us.

************
Dependencies
************

We rely on some third party packages, and for more information on how 
those work, see those packages themselves. For a complete list of dependencies, 
workspace package dependencies are listed in
robot_ws/src/3rdparty/scripts/install-dependencies.sh, workspace dependencies are listed
in the dockerfile and robot dependencies are located in 
/firmware/naoimage-snippets.

