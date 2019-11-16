.. _pc-setup-contributing:

#######################
PC Setup (Contributing)
#######################

*************
Getting Linux
*************

A Linux OS is required to work with the rUNSWift codebase.
`Ubuntu 18.04 LTS amd64 <http://releases.ubuntu.com/18.04/>`_ is the recommended OS.
You can either use a virtual machine, or dual boot your computer.

**Pick one of the following:**

.. toctree::
   gain_push_access_in_runswift_vm
   pc_setup_virtual_box
   pc_setup_dual_boot

.. note::
    The following distributions are known to work:

    - `Ubuntu 16.04 LTS amd64 <http://releases.ubuntu.com/16.04/>`_ (Need to disable black or install python3.6)
    - `Ubuntu 18.04 LTS amd64 <http://releases.ubuntu.com/18.04/>`_
    - `Ubuntu 19.04 amd64 <http://releases.ubuntu.com/19.04/>`_
    - `Debian 9 (amd64 & i386) <https://www.debian.org/>`_ (Need to disable black or install python3.6)
    - `Debian 10 (amd64 & i386) <https://www.debian.org/>`_ (ctc 2.1 uses glibc 2.6 and needs `vsyscall=emulate <https://tracker.debian.org/media/packages/l/linux/changelog-4.10~rc6-1~exp1>`_)

.. tip::
    Have at least 50GB storage and 4GB RAM.

.. warning::
    A virtual machine is more likely to experience slowness in compiling and running simulations.

*********************
Add SSH key to GitHub
*********************

#. Generating SSH key
    #. Open Terminal (Ctrl+Alt+T)
    #. Run :code:`ssh-keygen -t rsa -b 4096`
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
