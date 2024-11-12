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

Run the following command in a terminal of your computer to connect to Kodos. Replace *username* with *your Kodos account username*.

.. code-block:: bash

   $ ssh username@kodos.cse.unsw.edu.au

***************************
Running VNC Server in Kodos
***************************

Run :code:`vncserver -geometry <dim>` in Kodos such as

.. code-block:: bash

   $ vncserver -geometry 1920x893

Run :code:`vncserver --list` in Kodos to find your X Display No.

If the X Display No. is 3, for example, the Port No. should be :code:`5900 + 3`, that is, :code:`5903`.

As the Port No. has been obtained, run the following command in a terminal of your computer to connect to Kodos. Replace *5903* with *your Port No.* and *username* with *your Kodos account username*.

.. code-block:: bash

   $ ssh -L 5903:localhost:5903 username@kodos.cse.unsw.edu.au

**********
VNC Viewer
**********

Download a VNC Viewer such as `TightVNC <https://www.tightvnc.com/>`_ (recommended), `RealVNC <https://www.realvnc.com>`_ or `Remote Ripple <https://remoteripple.com>`_ and install it on your computer.

Run VNC Viewer in your computer with the VNC Server address being :code:`localhost:<X Display No.>` such as

.. code-block:: bash

   localhost:3

Then, you can see Kodos as a remote desktop from your computer screen.

***************
Troubleshooting
***************

This section is helpful only if a Terminal or Files window does not open on the remote desktop.

To open a terminal window in the remote desktop, run the following command in the terminal where your computer is connected to Kodos using SSH.

.. code-block:: bash

   $ env -i DISPLAY=:3 gnome-terminal

To open a Files window in the remote desktop, run the following command in the terminal where your computer is connected to Kodos using SSH.

.. code-block:: bash

   $ DISPLAY=:3 nautilus &


