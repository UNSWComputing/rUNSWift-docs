####################
*setup-venue* Script
####################

At a new venue, some wireless network settings must change. The *setup-venue* script
is a bash script that configures first-time settings on the robot.


The script is situated in ``$RUNSWIFT_CHECKOUT_DIR/bin/setup-game``, and can be executed by running

.. code-block:: bash

    $ setup-venue.sh

.. note::
    The script has to only be run once when switching venues

.. note::
    For the competition, the IP addresses in the range 10.0.18.0 - 10.0.18.255 are available to our team.
    Currently, the following convention is used by the team:

+-----------------------------------------------+-----------------------------+
|   Router                                      |  10.0.18.1                  |
+-----------------------------------------------+-----------------------------+
|   DHCP (dynamically assigned address)         |  10.0.18.2 - 10.0.18.99     |
+-----------------------------------------------+-----------------------------+
|   Robots on wifi                              |  10.0.18.100 - 10.0.18.199  |
+-----------------------------------------------+-----------------------------+
|   Team Laptops (if we need a static address)  |  10.0.18.200 - 10.0.18.255  |
+-----------------------------------------------+-----------------------------+

For robot IP suffixes, see `updateWlanSetup.py <https://github.com/UNSWComputing/rUNSWift/blob/master/utils/wifitools/updateWlanSetup.py>`_ .

For more info, see `setup-venue.config.sh <https://github.com/UNSWComputing/rUNSWift/blob/master/bin/setup-venue.config.sh>`_ .
