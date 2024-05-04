##################
NAO Setup
##################

.. note::

    In 2024, rUNSWift completely migrated their robot OS to Ubuntu. If you wish to see the old documentation for the
    Softbank-based OS visit https://runswift.readthedocs.io/en/2023/setup/nao_setup.html

In this guide, we will go through the process of setting up a fresh NAO robot for RoboCup SPL using rUNSWift's image.

Most of these instructions can be used to upgrade or reset robots as well.

The robots that return from repair will likely not need these instructions.

.. note::
 **You do not need to do this if are just setting up your environment!**

*****************
What's different?
*****************
Our robots have traditionally been running NAOqi OS. However, we recently transitioned our robots (and our tooling/software) to be compatible with Ubuntu 22.04 as a base image.

This offers several advantages. On top of being more familiar to most of us, it makes things a lot simpler from a technical perspective,
alongside allowing us to pursue new technical projects with a better chance of success such as the ongoing research into a migration to ROS/ROS2.

**************
Build rUNSWift
**************
Before doing anything, you should build ``runswift``. While technically optional, this will be useful later on, as the image
you create would automatically bake in the ``runswift`` executable if it exists. Make sure you follow the PC setup guide beforehand.


Use ``docker.ps1`` if you're on Windows.

.. code-block:: bash


    ./bin/docker.sh bin/build-runswift.sh


*****************
Download opn file
*****************

OpenNAO (opn) files are the image file for the NAO robot.

- For teams new to RoboCup SPL, please contact the RoboCup SPL Technical Committee (rc-spl-tc AT lists.robocup.org) as mentioned `here <https://spl.robocup.org/v6-support/>`_.

- If you're not aligned with RoboCup, please contact your regional NAO reseller, most likely either Softbank Robotics or United Robotics Group.


If you are on site at UNSW, running ``build-naoimage.sh`` will download the opn file for you as part of the image creation process.

For passwords, please :ref:`contact` us.

You can download them manually as follows:

.. code-block:: bash

    # 2.8 image (v6)
    rsync -P repository@runswift2.cse.unsw.edu.au:/var/www/html/opennao2/build-2.8.5.1x/nao-2.8.5.11_ROBOCUP_ONLY_with_root.opn .


.. warning::
    Due to software licensing between Softbank and RoboCup SPL, teams can't publicly release the NAOqi OS provided by Softbank.

****************************
Create a custom Ubuntu Image
****************************
We will now create a custom Ubuntu image, which will use the base Softbank image and add our own customisations on top.

The process is based off the NaoDevil's flasher. You can find the source code `here <https://github.com/NaoDevils/NaoImage>`_.

- Windows
    .. code-block:: powershell

        bin\docker.ps1 bin/build-naoimage.sh


- Mac/Linux
    .. code-block:: bash

        bin/docker.sh bin/build-naoimage.sh


Ensure you have Docker installed before continuing. This process will take a significant period if you are running for the first time.

For subsequent runs, you will have the option to save time by reusing the base Ubuntu image.
As long as you didn't make any changes to the root scripts (you are unlikely to as they are located inside of the NaoDevils code) you can continue with the saved base to save time.

******************
Flashing the Robot
******************

You have 2 options to flash the robot:


Create a Flashable USB (Recommended)
************************************

This approach is likely to work with the least amount of complications.

Using the output opn file (``softwares/image.opn``), you can either use the official Nao Flasher or ``dd`` on Linux/Mac to flash the USB.

If you wish to use the official Nao Flasher, follow the instructions on `Softbank's Documentation <http://doc.aldebaran.com/2-1/software/naoflasher/naoflasher.html>`_

You can also use the flash script in the bin directory to flash the USB using ``dd``.
    .. code-block:: bash

        # run without args to view the help menu
        ./bin/make-usb.sh


Once the USB is made, turn off the robot and plug the USB to the back of its head. Then, hold the chest button continuously until it turns blue.

Let go, and it should start flashing blue rapidly. The lights on the side of the head will tell you the flashing progress. Once it's done, the robot will automatically boot.

.. tip::
    If this step takes too long (>30 minutes) turn the robot off and retry flashing.

Network flash
****************
You can also flash over the network with the following script:

    .. code-block:: bash

        ./bin/flash-robot.sh <robot-hostname or ip>

Restarting the robot will then begin the flashing process (the script should also prompt you to do so)


*********************************
Robot Config, Name and Wifi Setup
*********************************
**If the robots are new** you will need to:

* Add the robot to ``robots/robots.cfg``
    * You can find its head id via ``cat /sys/qi/head_id`` after ``ssh <robot>``.
    * Note you can flash safely without adding the robot to this file, and discover the head ID by ``ssh <IP>`` the robot calls out after flashing, and running the ``cat`` command.

* Add ``<robot-name>`` to the list of robots in ``utils/webnao/src/common/dicts/robots.ts``
* Create a copy of the default ``.cfg`` file called ``<robot-name>.cfg`` in ``image/home/nao/data/configs/``
* Create a copy of the default ``.cfg`` file called ``<robot-name>.cfg`` in ``image/home/nao/data/configs/body/``

*********************************
Uploading rUNSWift
*********************************

The image by default should already have rUNSWift. You can check details about the flash by looking at ``image.commit.sha`` and ``image.build.time`` in the home dir.

To flash a new version, run:

.. code-block:: bash

    bin/nao_sync.sh <robot hostname or ip>

The robot should already be good to go with the IP specified in robots/robots.cfg for LAN and wifi in SPL_A

You can see the network settings in ``/etc/netplan`` directory. You can modify these files and then run ``sudo netplan apply`` to apply the changes.

However, we do have scripts to manage these files as we detail further down below. Therefore, you shouldn't really need to modify them yourself.

The default username and password for the robot after flashing is ``nao:nao``.
Save yourself the hassle of typing this out repeatedly and add your key to ``image/home/nao/.ssh/authorized_keys`` and flash.

*********************************
Troubleshooting
*********************************

.. tip::

    It's sometimes useful to just flash the base opn image if you experience issues with robot kinematics, but are confident there are no hardware issues.
    You can simply use the base image with the aforementioned flash methods to restore the default nao image, and then flash the custom image once you confirm
    things roughly work as expected on the base image.

.. tip::

    ``<hostname>`` is likely ``nao.local`` for new or factory reset robots. This could be used instead of the IP address during setup.

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

To play a game by the SPL Rules, the ``runswift`` executable needs to send packets of
information to, and respond to commands from, one specific soccer field's
`GameController <https://github.com/RoboCup-SPL/GameController3/>`_. Typically the
competition organisers will provide the list of field SSIDs and any other details
at the competition, for example ``SPL_A`` to ``SPL_E`` has been typical of RoboCup.

One way to do this is to use the change_field script located in bin.
You can also modify the WIFI network manually in the ``/etc/netplan`` directory and run ``sudo netplan apply`` if you're in a pinch.

.. code-block:: bash

    bin/change_field.py <robot hostname or ip> <field (e.g. SPL_A)>

You can also provide ``*`` to change_field to change the field of all robots in robots.cfg.

Note the robot is capable of maintaining an eth and wifi connection at the same time.

Please ensure to disconnect from the Game controller wifi during an active game you are not part of as per the rules.

.. code-block:: bash

    bin/change_field.py <robot hostname or ip> NONE

Providing NONE disables Wifi on the robot (makes it attempt to connect to NONE which doesn't exist)
