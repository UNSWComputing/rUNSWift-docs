################
Working Remotely
################

Some nao robots are always turned on in the Robotics Lab for working remotely via the Kodos server.

*****************************
Connecting to Kodos using SSH
*****************************

First, your computer should be connected to Kodos using SSH.

.. note::
    For creating your account on Kodos, please :ref:`contact` us.

Run the following command in a terminal of your computer to connect to Kodos.

.. code-block:: bash

   $ ssh -L 5903:localhost:5903 username@kodos.cse.unsw.edu.au

***************************
Running VNC Server in Kodos
***************************

Run :code:`vncserver -geometry <dim>` in Kodos such as

.. code-block:: bash

   $ vncserver -geometry 1920x893

Run :code:`vncserver -list` in Kodos to find your X Display NO.

**********
VNC Viewer
**********

Download VNC Viewer from `RealVNC <https://www.realvnc.com>`_ and install it on your computer.

Run VNC Viewer in your computer with the VNC Server address being :code:`localhost :<X Display NO>` such as

.. code-block:: bash

   localhost :3

Then, you can see Kodos as a remote desktop from your computer screen.

To open a terminal in the remote desktop, run the following command in the terminal where your computer is connected to Kodos using SSH.

.. code-block:: bash

   $ env -i DISPLAY=:3 gnome-terminal

To open a Files (File Explorer) in the remote desktop, run the following command in the terminal where your computer is connected to Kodos using SSH.

.. code-block:: bash

   $ DISPLAY=:3 nautilus &


