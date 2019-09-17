.. _pc-setup-contributing:

#######################
PC Setup (Contributing)
#######################

*************
Getting Linux
*************

A Linux OS is required to work with the rUNSWift codebase.
`Ubuntu 18.04 LTS <http://releases.ubuntu.com/18.04/>`_ is the recommended OS.

.. note::
    Installing an OS is beyond the scope of this wiki. The following distributions are also known to work:

    - `Ubuntu 16.04 LTS <http://releases.ubuntu.com/16.04/>`_
    - `Ubuntu 18.04 LTS <http://releases.ubuntu.com/18.04/>`_
    - `Ubuntu 19.04 <http://releases.ubuntu.com/19.04/>`_
    - `Debian 9 (64-bit & 32-bit) <https://www.debian.org/>`_

.. note::
    Have at least 30GB storage and 4GB RAM.

.. warning::
    A virtual machine is more likely to experience slowness in compiling and running simulations.

**************
Installing Git
**************

Run :code:`sudo apt-get install git`.

*********************
Add SSH key to Github
*********************

Follow the `Github Instructions <https://help.github.com/en/enterprise/2.15/user/articles/adding-a-new-ssh-key-to-your-github-account>`_.

******************
Cloning Repository
******************

Run :code:`git clone git@github.com:UNSWComputing/rUNSWift.git rUNSWift`

.. note::
    Your Github account must have access to the private rUNSWift repository to be able to clone it. To gain access, please :ref:`contact` us.

***********************
Build Environment Setup
***********************

Run :code:`rUNSWift/bin/build_setup.sh`.

.. note::
    For passwords, please :ref:`contact` us.

*******************
VirtualBox Settings
*******************

Storage Space - 30GB or more

System Memory (RAM) - 4GB or more

Number of Procesors - Equal to the number of cores on your System