#########
NAO Setup
#########

.. warning::
    Instructions here are not complete yet.

Follow these instructions to prepare Naos, that are brand new or have been
factory reset, to run the rUNSWift codebase.

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

Run

.. code-block:: bash

    nao_sync -s -h nao.local mario

.. note::
    Replace ``mario`` with the name of the new robot.
    Robot names should consist of lower case alphabets or numbers

.. tip::
    After plugging your work machine into your Nao via an ethernet cable, you can also use the Softbank web page at http://nao.local/ (username/password are nao/nao respectively) to change the Nao's name.

*************************
Places to add ``<NAME>``
*************************
#. ``<NAME>``.cfg in /image/home/nao/data/configs/ and /image/home/nao/data/configs/body/

    .. code-block:: 

        [player]
        number=2
        team=18
#. in ``source.sh`` add the <NAME> to the appropriate list of names on line 150 or 153 (approx)
#. Add the name and a new ip number in ``utils/wifitools/updateWlanSetup.py`` - The wifi IP will be zzz.zzz.18.1XX, where you set XX in the dictionary and zzz.zzz is usually ``10.0.*`` or ``192.168.*``. The idea is that the ethernet ip is .18.XX, and the wifi is .18.1XX for a given robot, but we use DHCP on ethernet and shouldn't use the same subnet for both wired and wireless anyway.
