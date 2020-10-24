###################
*setup-game* Script
###################

The script is situated in ``$RUNSWIFT_CHECKOUT_DIR/bin/setup-game``, and can be executed by running


.. code-block:: bash

    $ setup-game.sh

It is used to configure many robots for a game using the configuration set in ``$RUNSWIFT_CHECKOUT_DIR/bin/setup-game.config.sh``

**************
Example Output
**************

::

    Please read the following settings.
    ===============================================================
    # teams and players must be the same number of columns
    # be sure to use '' for blank robots
    teams=(    18     )
    p1s=(   gandalf )
    p2s=(   '' )
    p3s=(   ''     )
    p4s=(   '')
    p5s=(    '')
    # backup players
    # these arrays must exist
    # these arrays must be the same length as above
    # be sure to use '' for blank robots
    p6s=(      ''     )
    p7s=(      ''     )
    p8s=(      '' )
    p9s=(       ''    )
    p10s=(      ''    )
    ===============================================================
    Are the following configuration settings OK? [Y/n]
    Y
    ===============================================================
     [+] [ 0%] Updating configuration files
     [+] [ 1%] Checking available connections to robots
    Have you rebooted all the nao's? [Y/n]
    Y
    Have you made sure the jersey is on the goalie properly? [Y/n]
    Y
    Are you setting up on a competition field? [Y/n]
    N
    Warning: Permanently added 'gandalf.local' (ECDSA) to the list of known hosts.
     [+] [ 0%] gandalf: Setting up on team 18 and player 1
     [+] [ 0%] gandalf: Restarting wifi
     [+] [100%] Setup complete
    1/1 players synced: gandalf
    Ready to play.

.. note:: 
    Robot names must be lower case.
    To setup two teams enter space seperated values (no commas).
    
    For example, two teams might be configures as such: 
    ::
    
        teams=(  18 5    )
        p1s=( gandalf gimli )
        p2s=( '' squirt )
        p3s=( legolas '' )
        p4s=( '' '' )
        p5s=( '' '' )
        p6s=( '' '' )
        p7s=( '' '' )
        p8s=( '' '' )
        p9s=( '' '' )
        p10s=( '' '' )

.. note::
    The script must be run before every game

