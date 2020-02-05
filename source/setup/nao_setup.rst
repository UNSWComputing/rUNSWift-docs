#########
NAO Setup
#########

.. warning::
    Instructions here are not complete yet.
    
.. note::
    Follow these instructions to prepare Naos that are brand new or have been
    factory reset, to run the rUNSWift codebase. 
    
    **You do not need to do this if are just setting up your environment!**

Naoqi is the OS for the NAO.


*****************
Download opn file
*****************

OpenNao (opn) files are the image file for the Nao robot.
Download using

.. code-block:: bash

    rsync -P runswift@runswift2.cse.unsw.edu.au:/var/www/html/opennao2/build-2.8.5.1x/nao-2.8.5.11_ROBOCUP_ONLY_with_root.opn .

.. note::
    For passwords, please :ref:`contact` us.

.. warning::
    Due to software licensing between Softbank and RoboCup SPL, teams can't publicly release the Naoqi OS provided by Softbank.


****************
Create Naoqi USB
****************

#.  Follow the instructions on
    `Softbank's Documentation <http://doc.aldebaran.com/2-1/software/naoflasher/naoflasher.html>`_

    .. note::
        The 2.1-flasher also works with the 2.8-opn


****************
Flashing the NAO
****************

#. Insert the USB stick into the back of the robots head
#. Press and hold down the chest button on the Nao until it lights up blue
#. Wait until it says ``Ognak gnuk!`` and starts looking around

.. tip::
    If this step takes too long (>30 minutes) turn the robot off and retry flashing.

*********************************
Robot Config, Name and Wifi Setup
*********************************
If the robots are new you will still need to:

* Add ``<robot-name>`` to the list of robot names in ``$RUNSWIFT_CHECKOUT_DIR/bin/source.sh``
* Add ``<robot-name>`` and the ip address of the robot to ``utils/wifitools/updateWlanSetup.py``
* Create a copy of the default ``.cfg`` file called ``<robot-name>.cfg`` in ``$RUNSWIFT_CHECKOUT_DIR/image/home/nao/data/configs/``
* Create a copy of the default ``.cfg`` file called``<robot-name>.cfg`` in ``$RUNSWIFT_CHECKOUT_DIR/image/home/nao/data/configs/body/``

*********************************
Syncing the nao
*********************************
Finally, for all robots, run

.. code-block:: bash

    nao_sync -s 
