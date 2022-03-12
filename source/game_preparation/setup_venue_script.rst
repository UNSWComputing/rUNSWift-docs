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
    For the competition, the robot IP addresses will be in the range 10.0.18.100 - 10.0.18.199
    
    See `this file <https://github.com/UNSWComputing/rUNSWift/blob/master/bin/setup-venue.config.sh>`_ for more info.
