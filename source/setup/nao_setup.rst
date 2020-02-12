#########
NAO Setup
#########

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
Download then to your current working directory using

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
