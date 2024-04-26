#########
NAO Setup
#########

.. warning::

   This document is deprecated. Please refer to the new document `here <nao_setup_ubuntu.html>`__.

Follow these instructions to prepare brand new NAOs and add them to the rUNSWift codebase.

Most of these instructions can be used to upgrade or reset robots as well.

The robots that return from repair will likely not need these instructions.

.. note::
 **You do not need to do this if are just setting up your environment!**

`NAOqi OS is the OS for the NAO.  It is a GNU/Linux distribution based on Yocto.
<http://doc.aldebaran.com/2-8/dev/tools/opennao.html>`_


*****************
Download opn file
*****************

OpenNAO (opn) files are the image file for the NAO robot.

- For teams new to RoboCup SPL, please contact the RoboCup SPL Technical Committee (rc-spl-tc@lists.robocup.org) as mentioned `here <https://spl.robocup.org/v6-support/>`_.

- If you're not aligned with RoboCup, please contact Aldebaran.

- If you're a member of rUNSWift, download them to your current working directory using

.. code-block:: bash

    # 2.1 image (v4 and v5)
    rsync -P repository@runswift2.cse.unsw.edu.au:/var/www/html/opennao2/build-2.1.4.13/opennao-atom-system-image-2.1.4.13_2015-08-27.opn .
    # 2.8 image (v6)
    rsync -P repository@runswift2.cse.unsw.edu.au:/var/www/html/opennao2/build-2.8.5.1x/nao-2.8.5.11_ROBOCUP_ONLY_with_root.opn .

.. note::
    For passwords, please :ref:`contact` us.

.. warning::
    Due to software licensing between Softbank and RoboCup SPL, teams can't publicly release the NAOqi OS provided by Softbank.


****************
Create NAOqi USB
****************

#.  Follow the instructions on
    `Softbank's Documentation <http://doc.aldebaran.com/2-1/software/naoflasher/naoflasher.html>`_

    .. note::
        The 2.1 flasher also works with the 2.8 opn.  You can also just use dd on linux and mac.


****************
Flashing the NAO
****************

#. Turn off the NAO
#. Insert the USB stick into the back of the robots head
#. Press and hold down the chest button on the NAO until it lights up blue
#. Wait until it says ``Ognak gnuk!`` and starts looking around

.. tip::
    If this step takes too long (>30 minutes) turn the robot off and retry flashing.

*********************************
Robot Config, Name and Wifi Setup
*********************************
**If the robots are new** you will need to:

* Add ``<robot-name>`` to the list of robot names in ``$RUNSWIFT_CHECKOUT_DIR/bin/source.sh``
* Add ``<robot-name>`` and the ip address of the robot to ``utils/wifitools/updateWlanSetup.py``
* Create a copy of the default ``.cfg`` file called ``<robot-name>.cfg`` in ``$RUNSWIFT_CHECKOUT_DIR/image/home/nao/data/configs/``
* Create a copy of the default ``.cfg`` file called ``<robot-name>.cfg`` in ``$RUNSWIFT_CHECKOUT_DIR/image/home/nao/data/configs/body/``

*********************************
Patching the OS for rUNSWift
*********************************
Finally, for all robots, run

.. code-block:: bash

    nao_sync -s -h <hostname> <robot-name>

.. tip::

    ``<hostname>`` is likely ``nao.local`` for new or factory reset robots.

    Robots that are flashed without factory reset should retain their hostnames and you don't
    need to specify ``-h <hostname>`` and ``<robot-name>.local`` will be used automatically.

.. tip::

    Workaround: If this last step is causing trouble for you, try changing the hostname at
    the command line first, then syncing, for example:

.. code-block:: bash

    PC$ ssh nao@nao.local
    nao$ sudo nano /etc/hostname
    # Agree, then change the hostname from 'nao' to for example 'treebeard'
    # then reboot the robot and continue as normal, i.e.
    PC$ nao_sync -s treebeard
    PC$ nao_sync -rd treebeard
    # reboot again

*********************************
Connecting to GameController Wifi
*********************************

To play a game by the SPL Rules, the `runswift` executable needs to send packets of
information to, and respond to commands from, one specific soccer field's
`GameController <https://github.com/RoboCup-SPL/GameController3/>`_. Typically the
competition organisers will provide the list of field SSIDs and any other details
at the competition, for example `SPL_A` to `SPL_E` has been typical of RoboCup.

One way to set this up is to SSH into the robot and use the change field script, this is
analagous to connecting to a wifi hotspot, one needs to specify things like the
`SSID <https://www.lifewire.com/definition-of-service-set-identifier-816547>`_:

.. code-block:: bash

    PC$ ssh nao@treebeard.local
    # sudo bin/changeField.py <SSID>
    sudo bin/changeField.py SPL_E


Further considering the SPL Rules section on `Wireless Communications`, robots should be
changed off the field when not playing a game or on an unused field:

.. code-block:: bash

    # runswift is not a valid SPL SSID, so the Nao's WiFi should
    # disconnect and fail to connect at a competition
    sudo bin/changeField.py runswift

