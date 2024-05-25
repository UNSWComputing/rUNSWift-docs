.. _pc-setup-contributing:

#######################
PC Setup (Contributing)
#######################

These are setup instructions for contributing members of the team to setup their PC.

*************
Getting Linux
*************

A Linux OS is required to work with the rUNSWift codebase.
`Ubuntu 22.04 LTS amd64 <http://releases.ubuntu.com/22.04/>`_ is the recommended OS.
You can either use a virtual machine, or dual boot your computer.


**Pick one of the following:**

.. toctree::
   gain_push_access_in_runswift_vm
   pc_setup_virtual_box
   pc_setup_dual_boot
   pc_setup_wsl

.. tip::
    Have at least 50GB storage and 4GB RAM.

.. warning::
    A virtual machine is more likely to experience slowness in compiling and running simulations.

*********************
Add SSH key to GitHub
*********************

#. Generating SSH key
    #. Open Terminal (Ctrl+Alt+T)
    #. Run :code:`ssh-keygen -t ed25519 -C "your_email@example.com"`
    #. Hit enter three times
#. Add SSH key to GitHub by following `GitHub Instructions <https://help.github.com/en/enterprise/2.15/user/articles/adding-a-new-ssh-key-to-your-github-account>`_

******************
Cloning Repository
******************

Run the following commands to clone the rUNSWift repository

.. code-block:: bash

   $ sudo apt-get install git
   $ git clone git@github.com:UNSWComputing/rUNSWift.git rUNSWift

.. note::
    Your GitHub account must have access to the private rUNSWift repository to be able to clone it. To gain access, please :ref:`contact` us.

***********************
Build Environment Setup
***********************

Run the following command to setup the build environment.

.. code-block:: bash

   $ rUNSWift/bin/setup-build.sh


.. note::
    For passwords, please :ref:`contact` us.
