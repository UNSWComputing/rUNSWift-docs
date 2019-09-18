####
Kick
####

Each robot has slightly different motion dynamics, and require a lean offset when kicking, to kick reliably.

************
Instructions
************

In this example, we will use a robot with the head of mario and body of yoshi.

========= =========
Head name Body name
========= =========
mario     yoshi
========= =========

#.  Ensure ``bodyName`` is correct in ``image/home/nao/data/configs/mario.cfg``.

    .. code-block:: cfg

        [player]
        bodyName=yoshi

    .. note::
        Replace ``mario`` and ``yoshi`` with your robot's head and body names

#.
    To run the kick calibration procedure for the **left foot**,

    .. code-block:: bash

        $ runswift --calibration.kick 1 --kick.foot LEFT --kick.leanOffsetL 0.0

    To run the kick calibration procedure for the **right foot**,

    .. code-block:: bash

        $ runswift --calibration.kick 1 --kick.foot RIGHT --kick.leanOffsetR 0.0

#.  Place a ball in front of robot's kicking foot. Robot will kick the ball.

#.  Modify the ``leanOffsetL`` and ``leanOffsetR`` value until the kick doesn't fallover sideways.

    .. note::
        ``kick_lean_offset`` is in **degrees**. Increments of 1.0 degrees is recommended for initial tuning, and 0.5 degrees for finer tuning.

    .. tip::
        **Increase** ``kick_lean_offset`` to make the robot **lean more** onto the support foot, and vice versa.


#.  Copy the tuned ``leanOffsetL`` and ``leanOffsetR`` into ``image/home/nao/data/configs/body/yoshi.cfg``

    .. code-block:: cfg

        [kick]
        leanOffsetL=1.0
        leanOffsetR=-2.0

    .. note::
        Replace ``yoshi`` with your robot's body names


#.  Repeat procedure for both feet.
